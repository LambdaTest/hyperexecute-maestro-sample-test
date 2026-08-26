# Testing your app in multiple languages (iOS simulators)

Run the same Maestro suite against your app in several languages on HyperExecute,
**without changing the simulator's language**.

The language is requested per launch through Maestro's `launchApp` arguments. iOS
reads `-AppleLanguages` / `-AppleLocale` at process start — the same mechanism
Xcode's scheme setting "Application Language" uses.

```yaml
- launchApp:
    appId: org.wikimedia.wikipedia
    clearState: true
    clearKeychain: true
    arguments:
      AppleLanguages: "(fr)"
      AppleLocale: "fr_FR"
```

Because the device is never modified, the flows are order-independent and safe to
run back to back on a shared device.

## Files

| File | Purpose |
|---|---|
| `yaml/ios/ios-lang-en.yaml` | English — asserts `Get started` |
| `yaml/ios/ios-lang-fr.yaml` | French — asserts `Démarrer` |
| `yaml/ios/ios-lang-ja.yaml` | Japanese — asserts `次へ` |
| `maestro-test/discover-iOS-lang.txt` | the test list — one flow per line |
| `yaml/ios/ios-simulator-language.yaml` | HyperExecute job config |
| `maestro-test/sample.zip` | the sample app — Wikipedia for iOS, which ships 200+ localizations |

Each flow asserts its own language marker **is** visible and the other languages'
markers are **not**. The negative assertions matter: the job keeps one device across
tests, so the previous test's app can still be running when the next begins.
Asserting only "my language is visible" would let leaked state pass quietly.

## Run it

```bash
# 1. credentials
export LT_USERNAME=<your-username>
export LT_ACCESS_KEY=<your-access-key>

# 2. upload the sample app and copy the returned lt:// id
curl -u "$LT_USERNAME:$LT_ACCESS_KEY" \
  -X POST "https://manual-api.lambdatest.com/app/upload/virtualDevice" \
  -F "appFile=@maestro-test/sample.zip" \
  -F "name=Wikipedia-localized-sample"

# 3. paste it into yaml/ios/ios-simulator-language.yaml as framework.args.appId

# 4. run
./hyperexecute \
  --user "$LT_USERNAME" \
  --key  "$LT_ACCESS_KEY" \
  --config yaml/ios/ios-simulator-language.yaml \
  --download-artifacts
```

App ids are per-account — an id copied from elsewhere will not resolve for you. A
stale or foreign id fails during device setup with a generic error, because the app
install happens as part of that stage. If setup fails unexpectedly, re-upload the
app before looking further.

Screenshots come back under `artifacts/` and are the evidence the language actually
changed.

To run a single language, edit `maestro-test/discover-iOS-lang.txt`.

## Using your own app

1. Upload your build (`.zip` of a `.app` for simulators, `.ipa` for real devices —
   use `/app/upload/realDevice` for the latter).
2. Put the returned id in `framework.args.appId`.
3. Change `appId:` in the flows to your bundle id, and replace the asserted strings
   with text your app actually shows in each language.

## What your app needs

Setting `AppleLanguages` is only a **preference**. iOS resolves it against the
languages your app actually ships:

- **Translations require localization resources** (`.lproj` folders or a String
  Catalog) and strings routed through `NSLocalizedString` / `String(localized:)`.
  An app that ships only English renders English no matter which language is
  requested. Hardcoded strings never translate.
- **Date, number and currency formatting follows `AppleLocale` regardless** — even a
  non-localized app renders `€1 234,50` for `fr_FR`.
- Give elements stable, language-independent `accessibilityIdentifier`s and match on
  `id:` for navigation, keeping text assertions for the translations you are actually
  testing. One flow then covers every language.

## Good to know

- **System permission dialogs are not affected.** Launch arguments apply to your app's
  process; permission alerts are drawn by iOS itself and follow the device language.
- **Do not copy this pattern to Android.** The same YAML is valid there, but Maestro
  passes `arguments` as intent extras rather than locale settings — the test would pass
  while nothing changed. Android needs a different mechanism.
- Verified with Maestro `2.6.1`, the version pinned in `maestro-test/setup-script-iOS.sh`.
