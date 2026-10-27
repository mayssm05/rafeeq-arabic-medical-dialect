# Rafiq | تطبيع اللهجة الطبية السعودية

مشروع بحثي/تعليمي لاستكشاف تحويل العبارات الطبية باللهجة السعودية إلى عربية مبسطة مع الحفاظ على المعنى. التصنيف المرتبط بالقسم الطبي وُضع للتجارب فقط؛ النظام ليس أداة تشخيص أو فرز طبي.

## الداتاسيت

الإصدار V2 يتكوّن من 493 مثالًا أساسيًا و72 مثالًا اصطناعيًا موجّهًا أُضيفت إلى التدريب: 565 مثالًا إجمالًا (459 تدريب، 57 تحقق، 49 اختبار). بطاقة الداتاسيت تصف سير العمل بأنه جمع ومراجعة يدوية للمفردات مع أمثلة صيغت بشريًا وبمساعدة الذكاء الاصطناعي.

الداتاسيت منشور على [Hugging Face](https://huggingface.co/datasets/Mayssm/rafeeq-arabic-medical-dialect) بترخيص [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). أُحيل إلى النسخة المنشورة بدل تكرار النصوص الطبية والتوقعات لكل مثال في هذا المستودع.

## التدريب والتقييم

استُخدم ASL-4B-v1 مع LoRA/QLoRA وضبط دقيق موجّه. نسخة الـnotebook هنا أُزيلت منها مخرجات الخلايا القديمة؛ وهي مُعدّة لـGoogle Colab، وتحتاج ملفات البيانات والأوزان في المسارات المتوقعة. الأوزان غير مرفقة بهذا المستودع، ولم يُنفّذ الـnotebook ضمنه. راجع كود النموذج البعيد قبل تشغيل الأسطر التي تستخدم `trust_remote_code=True`.

النتائج المرفقة على مجموعة اختبار من 49 مثالًا:

| المقياس | النتيجة |
| --- | ---: |
| BLEU | 68.44 |
| ROUGE-L | 0.7741 |
| chrF | 79.41 |
| Token F1 | 0.7768 |
| Strict Exact Match | 0.4898 (24/49) |

**قيد مهم:** صُممت أمثلة التحسين الموجّه بعد مراجعة أخطاء مجموعة الاختبار. لم تُنسخ جمل الاختبار حرفيًا، لكن مفردات الاختبار أثّرت في أمثلة التدريب؛ لذلك لا تمثل هذه النتيجة اختبارًا مستقلًا لقدرة النموذج على التعامل مع مفردات لم يرها سابقًا. مقاييس التطابق النصي لا تثبت الدقة الطبية أو السلامة السريرية.

## العرض التفاعلي

يتوفر [عرض الواجهة](https://rafeeeq.netlify.app/) وملف [Frontend Demo PDF](docs/frontend-demo.pdf). وفقًا لوصف العرض، الواجهة تستخدم أمثلة جاهزة ولا تتصل حاليًا بواجهة خلفية للنموذج. لم يُرفق مصدر الواجهة بهذا المستودع.

## محتويات المستودع

- `notebooks/RafiQ_Train.ipynb` — نسخة تدريب منقحة، مع حذف مخرجات الخلايا.
- `results/v2_metrics.csv` — المقاييس الإجمالية.
- `results/v2_training_history.csv` — سجل التدريب.
- `docs/frontend-demo.pdf` — وصف عرض الواجهة.

## الترخيص والمراجع

- الداتاسيت: CC BY 4.0؛ راجع بطاقة Hugging Face للترخيص والإسناد.
- النموذج الأساسي: [SAAI ASL-4B-v1](https://huggingface.co/saai-sa/ASL-4B-v1)، بترخيص Apache 2.0 بحسب بطاقة النموذج.
- لم يُرفق ترخيص منفصل لكود المشروع في المواد المستلمة.

---

## English

Rafiq is a research and learning project exploring the normalization of Saudi Arabic medical-dialect expressions into simpler Arabic while preserving meaning. The medical-department label is auxiliary and intended for experiments only; this is not a diagnostic or medical-triage system.

### Dataset

V2 contains 493 base examples plus 72 targeted synthetic examples added to training: 565 total (459 train, 57 validation, 49 test). The dataset card describes manual vocabulary curation and a mix of human-authored and AI-assisted example generation.

The dataset is already published on [Hugging Face](https://huggingface.co/datasets/Mayssm/rafeeq-arabic-medical-dialect) under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This repository links to that release instead of duplicating medical text and per-example predictions.

### Training and evaluation

The training notebook fine-tunes ASL-4B-v1 with LoRA/QLoRA. The public copy has saved cell outputs cleared. It was prepared for Google Colab and expects the data and model checkpoint in configured paths; the checkpoint is not included and the notebook has not been run as part of this repository. Review the remote model code before running cells that use `trust_remote_code=True`.

Reported results on the 49-example test set:

| Metric | Result |
| --- | ---: |
| BLEU | 68.44 |
| ROUGE-L | 0.7741 |
| chrF | 79.41 |
| Token F1 | 0.7768 |
| Strict Exact Match | 0.4898 (24/49) |

**Important evaluation limitation:** Targeted augmentation examples were designed after reviewing errors on the test set. Exact test sentences were not copied, but test vocabulary informed training examples. The resulting score is therefore not an independent test of generalization to unseen vocabulary. Text-overlap metrics do not establish medical accuracy or clinical safety.

### Interactive demo

The [frontend demo](https://rafeeeq.netlify.app/) and [demo PDF](docs/frontend-demo.pdf) are included. The supplied description says the frontend displays prepared examples and is not currently connected to a model backend. Frontend source code was not among the supplied files.

### Files

- `notebooks/RafiQ_Train.ipynb` — training notebook with saved outputs cleared.
- `results/v2_metrics.csv` — aggregate metrics.
- `results/v2_training_history.csv` — training log.
- `docs/frontend-demo.pdf` — frontend demo overview.

### Licenses and references

- Dataset: CC BY 4.0; see the Hugging Face card for attribution details.
- Base model: [SAAI ASL-4B-v1](https://huggingface.co/saai-sa/ASL-4B-v1), listed under Apache 2.0 on its model card.
- No separate license for the project code was included in the supplied materials.
