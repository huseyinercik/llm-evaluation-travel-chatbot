# Travel Chatbot Answer Relevance Testi

Bu klasör, travel chatbot cevaplarının kullanıcı sorusuyla ne kadar ilgili
olduğunu ölçmek için kullanılır.

## Gereksinimler

- Node.js ve `npx`
- Chatbot endpoint'i için `HF_TOKEN` ve `HF_Endpoint`
- Answer relevance judge ve embedding işlemleri için `OPENAI_API_KEY`

Değişkenler proje kökündeki `.env` dosyasından yüklenir.

`.env` örneği:

```dotenv
OPENAI_API_KEY=<openai-api-key>
HF_TOKEN=<hugging-face-token>
HF_Endpoint=https://<hugging-face-space>.hf.space/chat
```

## Testi çalıştırma

Proje kökünden aşağıdaki komutları çalıştırın:

```bash
cd travel-chatbot/answer-relevance
npx promptfoo@latest eval --env-file ../../.env -c answer-relevanceconfig.yaml --no-cache
```

Konfigürasyon 100 testi iki eşzamanlı istekle çalıştırır; endpoint yavaşsa
`evaluateOptions.maxConcurrency` değeri düşürülebilir.

Sonuçları Promptfoo arayüzünde görüntülemek için:

```bash
npx promptfoo@latest view
```

`--no-cache` seçeneği, önceki sonuçların kullanılmasını engeller ve güncel
test/config sonuçlarının yeniden üretilmesini sağlar.

## Dosyalar

- `answer-relevanceconfig.yaml`: Answer relevance test konfigürasyonu
- `input.yaml`: 100 test sorusu
- `providers.yaml`: Travel chatbot API provider tanımı
