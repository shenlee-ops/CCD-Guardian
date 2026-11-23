CCD GUARDIAN 4.0  |  Native Windows 64-bit build
==============================================

START HERE
1. Extract this ZIP to a NEW folder, separate from v3.
2. Double-click CCDGuardian.exe (not the .c source file).
3. Launch your game. Use the search bar or the "Likely games" filter.
4. Select its process to inspect CPU load, memory, threads, uptime and allowed CCDs.

WHAT THIS VERSION ADDS
- Restyled near-grayscale UI: charcoal/gray/white, muted sage for the V-Cache CCD,
  neutral gray-blue for the frequency CCD, subdued amber/red for warnings/errors.
- Larger, scrollable running-application list and name/path search.
- Actual overall CPU BUSY percentage of each CCD (not process-specific placement).
- Optional per-game Windows scheduler trace (kernel ETW context switches) showing
  estimated V-Cache vs frequency CCD execution of a selected process's threads.
- Per-process CPU, RAM, thread count, uptime, priority and process path.
- Process CPU trend chart, advanced affinity mask information.
- Compact monitoring view, live pause/refresh, diagnostics export and copy details.
- Exact-executable-path saved CCD preferences. Optional auto-apply within this
  session, OFF by default and enabled only after explicit confirmation.
- Manual Pin V-Cache, Pin Frequency, and Restore Original controls.

HOW TO MEASURE WHERE A GAME IS REALLY EXECUTING
1. Select a game in the left process list.
2. Click "Start precise trace" near the top of the list.
3. Confirm the prompt. Depending on Windows permissions, you may need to close
   the app and run CCDGuardian.exe as administrator to start the trace.
4. Play the game to produce scheduling activity. The inspector will show an
   ESTIMATED split of observed scheduled runtime between CCDs, updated every ~3s.
5. Click "Stop scheduler trace" when finished.
This trace is opt-in. Kernel context-switch tracing uses system-wide telemetry
and has some overhead. It does not pin or otherwise modify your game.
Some Windows builds, security settings or anti-cheat software may block it.
No measurements will be claimed when the trace is unavailable.

SAFETY NOTES
- Reading CPU affinity alone does NOT prove where game threads actually run.
- AMD/Windows game scheduling and core parking may be working correctly even
  when affinity lists both CCDs.
- A saved game preference does nothing by itself. Auto profiles are OFF by
  default; if enabled, they can change process affinity without repeated prompts
  for exact-path matches DURING THAT SESSION ONLY.
- Manual pinning changes the game's allowed processors; it may reduce performance
  or conflict with anti-cheat. Every manual change asks for confirmation.
- "Restore original" is available while this app remains open and the game is
  still running. If you close the app while a game is pinned, the game's current
  affinity is not automatically reverted. You can relaunch the game to reset it.
- Application looks for exactly one 96 MiB and one 32 MiB L3 cache domain. When
  topology is not verified, pinning is disabled rather than guessing CCD order.
- Profiles are saved to %LOCALAPPDATA%\CCDGuardian\profiles.dat.
- Export diagnostics writes a text file into the EXE directory when writable,
  otherwise the Windows TEMP directory. Review its contents before sharing.
- CCD Guardian does not install drivers, modify registry startup entries, or
  silently change affinity when launched.

DEVELOPMENT / LIMITATIONS
- This is an UNSIGNED test executable. Windows may display an unrecognized-app
  warning. Only run software you trust; inspect the included source if desired.
- Compiled as a Windows x64 GUI executable (PE32+) with clang-cl + lld-link.
- The executable and imports have been statically verified; this environment
  cannot perform a live Windows 11 / Ryzen 9 9950X3D runtime test.
- Scheduler measurements are estimates from traced context switches and a
  periodically refreshed selected-process thread list, not perfect or exhaustive.
- Full-screen anti-cheat protected titles may deny process inspection or tracing.
- The app uses a lightweight immediate-mode Win32 GUI; no .NET or PowerShell.

FILES
CCDGuardian.exe      - run this
CCDGuardian-source.c - auditable source
README.txt           - this document
LICENSE.txt          - MIT license for included application source
