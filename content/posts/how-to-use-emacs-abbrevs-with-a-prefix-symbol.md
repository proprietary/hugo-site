+++
title = 'How to Use Emacs Abbrevs With a Prefix Symbol'
date = 2019-01-27T01:42:31-07:00
draft = false
+++

## Abbrevs in Emacs and its limited namespace problem
[Abbrevs](https://www.gnu.org/software/emacs/manual/html_node/elisp/Abbrevs.html) in Emacs are tables of expansions of short words to arbitrary longer strings. This is commonly called a “text replacement” in other editors. The canonical example of an abbrev/text replacement[fn:meta_joke] is “omw” → “on my way”. Of course you could make more sophisticated abbrevs---e.g., replace a few letters with lines of `#include <stdio.h>` type boilerplate.

A limitation I encountered with this was how easily my abbrevs could clash with normal text. Since abbrevs can only be alphanumeric, and you can’t put punctuation in the abbrev, the number of abbrevs you can have is limited to just character combinations like “zbt”, “dfje”, ..., that don’t clash with words you might actually write. You can easily run out. You also can’t have a convenient single character expand to your text macro: “b” → “<b></b>” would be impossible.

## More possibilities with prefixed abbrevs
The solution was to hack abbrevs to be namespaced under a prefix symbol. I like using “$”, so I could use something like “$ps” → “public static ” whereas typing “ps” wouldn’t trigger the expansion since it is not preceded by my prefix character.

Here’s the macro:

```lisp
    (defmacro make-prefixed-abbrev-table (prefix-char abbrev-spec)
      "Creates and loads an abbrev-table with abbrevs prefixed by a PREFIX-CHAR. The abbrev table is loaded into local buffer scope.
    
    RETURNS the new abbrev table.
    
    Abbrev tables by themselves can only match plain words, like 'abc'. With this macro, you can prefix words with a special character, like '$', so that 'abc' would only expand to its expansion if you wrote '$abc'. This makes it harder to unintentionally write an abbrev because the prefix character makes it unlikely.
    (defmacro make-prefixed-abbrev-table (prefix-char abbrev-spec)
      "Creates and loads an abbrev-table with abbrevs prefixed by a PREFIX-CHAR. The abbrev table is loaded into local buffer scope.
    
    RETURNS the new abbrev table.
    
    Abbrev tables by themselves can only match plain words, like 'abc'. With this macro, you can prefix words with a special character, like '$', so that 'abc' would only expand to its expansion if you wrote '$abc'. This makes it harder to unintentionally write an abbrev because the prefix character makes it unlikely.
    
    Example:
    
    (make-prefixed-abbrev-table ?$ '((\"epsilon\" \"ε\")))
    
    Then when you're writing:
    
    $epsilon → ε"
      (assert (and (char-or-string-p prefix-char)
                   (or (not (sequencep prefix-char))
                       (= 1 (length prefix-char))))
              t
              "PREFIX-CHAR must either be a character or a string one character long")
      `(prog1 (define-abbrev-table 'local-abbrev-table
                ,abbrev-spec
                :case-fixed t
                :regexp ,(concat "\\" (char-to-string prefix-char) "\\([a-zA-Z0-9]+\\)")
                )
         (add-function :around (local 'abbrev-expand-function)
                       #'(lambda (expand-fn)
                           (let ((prev-point (save-excursion
                                               (backward-word-strictly)
                                               (point))))
                             (when (funcall expand-fn)
                               (save-excursion
                                 (goto-char prev-point)
                                 (delete-char 1))))))))
```

Usage:

```lisp
    (defun activate-my-writing-abbrevs ()
      (interactive)
      (make-prefixed-abbrev-table ?$ ;; use $ as prefix symbol
                                  '(
                                    ("beta" "β")
                                    ("alpha" "α")
                                    ("Alpha" "Α")
                                    ("crylaugh" "😂")
                                    ("rofl" "🤣")
                                    )))
```

When editing your file, ~M-x activate-my-writing-abbrevs~ to see it in action.
