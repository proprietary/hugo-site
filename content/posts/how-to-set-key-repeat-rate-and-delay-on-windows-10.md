+++
title = 'How to Set Key Repeat Rate and Delay on Windows 10'
date = 2019-01-19T01:50:53-07:00
draft = false
+++

## Problem
You can’t set the key repeat rate beyond a certain amount in the Windows 10 Control Panel. There are some recommendations to change some registry settings, but even that doesn’t work; it only changes the setting in the Control Panel that you could change anyway.

I like keys repeating very quickly because it allows quick navigation in text files. GNU/Linux desktop environments already let you choose any repeat rate you want. On Windows I wanted this too, so here’s how you can do that.

## Solution
This is the only way to change the keyboard repeat settings beyond what you are allowed to change it to in the Control Panel. You need to compile and run this C++ code.

Install and use [Visual Studio](https://visualstudio.microsoft.com/downloads/) for the smoothest experience. Then execute the binary from command line like this: `name_of_your_binary <delay ms> <repeat ms>`.

```c++
#include <windows.h>
#include <stdlib.h>
#include <stdio.h>

BOOL parseDword(const char* in, DWORD* out)
{
  char* end;
  long result = strtol(in, &end, 10);
  BOOL success = (errno == 0 && end != in);
  if (success)
	{
      *out = result;
	}
  return success;
}

int main(int argc, char* argv[])
{
  FILTERKEYS keys { sizeof(FILTERKEYS) };

  if (argc == 3
      && parseDword(argv[1], &keys.iDelayMSec)
      && parseDword(argv[2], &keys.iRepeatMSec))
	{
      printf("Setting keyrate: delay: %d, rate: %d\n", (int)keys.iDelayMSec, (int)keys.iRepeatMSec);
      keys.dwFlags = FKF_FILTERKEYSON | FKF_AVAILABLE;
	}
  else if (argc == 1)
	{
      puts("No parameters given, so displaying the current value of the key rate delay and speed settings:");
      if (!SystemParametersInfo(SPI_GETFILTERKEYS, sizeof(FILTERKEYS), (LPVOID)&keys, 0)) {
        fprintf(stderr, "System call ``SystemParametersInfo(SPI_GETFILTERKEYS, …)'' failed.");
        return 2;l
      }
      printf("delay: %d, rate: %d\n", static_cast<int>(keys.iDelayMSec), static_cast<int>(keys.iRepeatMSec));
      puts("Usage: keyrate <delay ms> <repeat ms>\nCall with no parameters to show the current setting.");
      return 0;
	}
  else
	{
      puts("Usage: keyrate <delay ms> <repeat ms>\nCall with no parameters to show the current setting.\n\nN.B.: I recommend the settings delay=200 and repeat=6");
      return 0;
	}

  if (!SystemParametersInfo(SPI_SETFILTERKEYS, sizeof(FILTERKEYS), (LPVOID)&keys, 0))
	{
      fprintf(stderr, "System call failed.\nUnable to set keyrate.");
	}
  printf("delay: %d, rate: %d\n", (int)keys.iDelayMSec, (int)keys.iRepeatMSec);

  return 0;
}
```
