# settings.json

基本はデフォルトに体を慣らしたほうが便利。どうしても許せないとこだけ変えとく。
別に手書きしないでコピーするけど、どっかで手動で書く必要があったとき用。

```js
{
    // サジェストが勝手に選択されるのウザいので切っとく。必要な時だけ呼ぶ。
    "editor.acceptSuggestionOnCommitCharacter": false,
    "editor.acceptSuggestionOnEnter": "off",

    // テレメトリ。別にどっちでもいいけど切っとく。
    "telemetry.enableCrashReporter": false,
    "telemetry.enableTelemetry": false,

    // Markdownの改行を無視しない。Qiitaと同じこっちのほうが好み。
    "markdown.preview.breaks": true,

    // タブサイズは2。
    "editor.tabSize": 2,

    // スタートアップ画面は無し。
    "workbench.startupEditor": "newUntitledFile",
}
```