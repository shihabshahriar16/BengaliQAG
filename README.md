# Abstract
The scarcity of comprehensive, high-quality Question-Answering (QA) datasets in low-resource languages
has greatly limited the progress of research on QA for these languages. This has inspired research on
Question-Answer Generation (QAG) which seeks to synthetically generate QA pairs and minimize the human
effort required to compile labeled datasets. In this paper, we present the first QAG pipeline for the
Bengali language, which consists of an answer span extraction model, a question generation model, and
roundtrip consistency filtering to discard inconsistent QA pairs. To train our QAG pipeline, we
translate SQuAD1.1 and SQuAD2.0 using the state-of-the-art NLLB machine translation model and accurately
mark the answer spans using a novel embedding-based answer alignment algorithm to construct two Bengali
QA datasets that we show are superior to the only two existing machine-translated datasets in terms of
quality and quantity. We use our QAG pipeline to generate more than 170,000 QA pairs to build BanglaQA,
a synthetic QA dataset from 16,000 Bengali news articles spanning 5 different news categories. We
demonstrate the quality of BanglaQA by human evaluation on a variety of metrics. The best performing
model among several baselines on our dataset achieves an F1 score of 86.14 falling behind human
performance of 95.72 F1. Our codebase and curated datasets are publicly available at
https://github.com/shihabshahriar16/BengaliQAG.git

## Datasets
1. [```BanglaQA Test Dataset```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/BanglaQA_Dataset/test_BanglaQA.json)
2. [```BanglaQA Train Dataset```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/BanglaQA_Dataset/train_BanglaQA.json)
3. [```BanglaQA Validation Dataset```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/BanglaQA_Dataset/val_BanglaQA.json)

An example of the dataset is shown below:
```json
{
  "data": [
    {
      "id": "1",
      "title": "sports",
      "context": "ব্রাজিলের ব্রুনো সোরেসের সঙ্গেজুটি বেঁধে ভারতীয় টেনিস তারকা জিতেছেন প্রথমবারের মতো ইউএস ওপেনের একটা শিরোপা।",
      "question": "কে ভারতীয় টেনিস তারকাকে ইউএস ওপেনের শিরোপা জিততে সাহায্য করেছে?",
      "answers": {
        "text": ["ব্রুনো সোরেসের"],
        "answer_start": [10]
      }
    }
  ]
}
```

## Translation
1. [```NLLB_translate_squad1.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/NLLB_translate_squad1.ipynb)
\: Translates the SQuAD1.1 to Bengali
2. [```NLLB_translate_squad2.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/NLLB_translate_squad2.ipynb)
\: Translates the SQuAD2.0 to Bengali (Requires the translated SQuAD1.1 dataset)


## Preprocessing
1. [```Preprocess_translated_squad_QAG.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/Preprocess_translated_squad_QAG.ipynb)
\: Preprocesses the translated dataset
2. [```BARD_context_selection.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/BARD_context_selection.ipynb)
\: Selects a specified number of contexts from the BARD dataset

## Question Answer Generation (QAG)
1. [```T5_answer_span_extraction.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/T5_answer_span_extraction.ipynb)
\: Trains the answer extraction model and runs inference on that
2. [```QG_with_appended_answer.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/QG_with_appended_answer.ipynb)
and [```QG_for_impossible_answer.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/QG_for_impossible_answer.ipynb) 
\: Trains the QG models for answerable and unanswerable questions
3. [```QA_on_translated_squad.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/QA_on_translated_squad.ipynb)
\: Trains the QA models on the condition that the datasets and models are available
4. [```QAG _dataset_generation.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/QAG%20_dataset_generation.ipynb)
and [```QAG _dataset_generation_adding_impossible_ans.ipynb```](https://github.com/shihabshahriar16/BengaliQAG/blob/main/QAG%20_dataset_generation_adding_impossible_ans.ipynb) 
\: Generates QA datasets