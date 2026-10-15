# Travel Chatbot Factuality Testi

Bu klasör, travel chatbot cevaplarını referans cevaplarla karşılaştırarak
factuality değerlendirmesi yapmak için kullanılır.

## Gereksinimler

- Node.js ve `npx`
- Chatbot endpoint'i için `HF_TOKEN`
- Judge modeli (`openai:gpt-5`) için `OPENAI_API_KEY`

Proje kökünde (`../../.env`) aşağıdaki değişkenler bulunmalıdır:

```bash
OPENAI_API_KEY=<openai-api-key>
HF_TOKEN=<hugging-face-token>
```

`.env` dosyasını git'e eklemeyin ve anahtarları paylaşmayın.

## Factuality testini çalıştırma

Önce bu klasöre geçin:

```bash
cd travel-chatbot/factuality
```

Testi proje kökündeki `.env` dosyasını yükleyerek ve cache kullanmadan çalıştırın:

```bash
npx promptfoo eval --env-file ../../.env -c factualityconfig.yaml --no-cache
```

Sonuçları Promptfoo UI üzerinde görüntülemek için:

```bash
npx promptfoo view
```

`--no-cache` seçeneği, önceki judge sonuçlarının tekrar kullanılmasını önler.
Bu nedenle Türkçe judge açıklaması gibi config değişikliklerinin yeni sonuçlara
yansımasını sağlar.

## Kullanılan dosyalar

- `factualityconfig.yaml`: Promptfoo değerlendirme konfigürasyonu ve factuality judge ayarları
- `inputs.yaml`: Test soruları ve beklenen cevaplar
- `providers.yaml`: Travel chatbot API provider tanımı
