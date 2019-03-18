# language-evaluation (Experimental)
Collection of evaluation code for natural language generation.

## Metrics
- `CocoEvaluator`: coco-caption (BLEU1-4, METEOR, ROUGE, CIDEr, SPICE)
- `RougeEvaluator`: sentence-level rouge (ROUGE-1, ROUGE-2, ROUGE-L with f-measure)
- `Rouge155Evaluator`: summary-level rouge (ROUGE-1, ROUGE-2, ROUGE-L with f-measure)

## Requirements
- Java 1.8.0+ (used by coco-caption evaluator)
- Python 3.6+
- `libxml-parser-perl` (used by ROUGE.1.5.5.pl)

## Installation and Usage

Install external dependencies (e.g. Java 1.8.0+, `libxml-parser-perl`):
```bash
# Oracle Java
sudo add-apt-repository ppa:webupd8team/java
sudo apt upadte
apt-get install oracle-java8-installer

# libxml-parser-perl
sudo apt install libxml-parser-perl
```

Then run:
```bash
pip install git+https://github.com/bckim92/language-evaluation.git
python -c "import language_evaluation; language_evaluation.download('coco')"
```

Python API (or see [language_evaluation_test.py](https://github.com/bckim92/language-evaluation/blob/master/language_evaluation_test.py)):
```python
import language_evaluation
from pprint import PrettyPrinter
pprint = PrettyPrinter().pprint

predicts = ['i am a boy', 'she is a girl']
answers = ['am i a boy ?', 'is she a girl ?']

evaluator = language_evaluation.CocoEvaluator()
results = evaluator.run_evaluation(predicts, answers)
pprint(results)
# {'Bleu_1': 0.9999999998823529,
#  'Bleu_2': 0.8944271908911816,
#  'Bleu_3': 0.7174075809792958,
#  'Bleu_4': 0.563321871690505,
#  'CIDEr': 6.308531746031747,
#  'METEOR': 0.5128174590570939,
#  'ROUGE_L': 0.8285714285714285,
#  'SPICE': 0.6111111111111112}

evaluator = language_evaluation.RougeEvaluator()
results = evaluator.run_evaluation(predicts, answers)
pprint(results)
# {'rouge1': 1.0,
#  'rouge2': 0.3333333333333333,
#  'rougeL': 0.75}

evaluator = language_evaluation.Rouge155Evaluator(num_parallel_calls=5)
results = evaluator.run_evaluation(predicts, answers)
pprint(results)
# {'rouge1': 1.0,
#  'rouge2': 0.3333333333333333,
#  'rougeL': 0.75}
```

## Notes
- TODOs
  - Support more metrics (e.g. embedding-based)
  - Support command-line interface
  - Support full functionality and configuration for rouge
  - Implement summary-level rouge scorer in pure python
  - Add tests & CI

## Related Projects
- [tylin/coco-caption](https://github.com/tylin/coco-caption)
- [bckim92/coco-caption-py3](https://github.com/bckim92/coco-caption-py3)
- [Maluuba/nlg-eval](https://github.com/Maluuba/nlg-eval)
- [google-research/google-research/rouge](https://github.com/google-research/google-research/tree/master/rouge)
- [bheinzerling/pyrouge](https://github.com/bheinzerling/pyrouge)

## License
See [LICENSE.md](LICENSE.md).
