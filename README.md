# TtsApplication
[このサンプル通りにやるとできる](https://serge-hulne.medium.com/how-to-do-text-to-speech-the-easy-way-with-android-kotlin-compose-2024-628015d4c5c2)

日本語の対応をするには、JAPANと書く
```kt
@Composable
fun rememberTextToSpeech(): MutableState<TextToSpeech?> {
    val context = LocalContext.current
    val tts = remember { mutableStateOf<TextToSpeech?>(null) }
    DisposableEffect(context) {
        val textToSpeech = TextToSpeech(context) { status ->
            if (status == TextToSpeech.SUCCESS) {
                tts.value?.language = Locale.JAPAN
            }
        }
        tts.value = textToSpeech

        onDispose {
            textToSpeech.stop()
            textToSpeech.shutdown()
        }
    }
    return tts
}
```
