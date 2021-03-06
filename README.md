# DC - Diagnostic Captioning
Based on [A Survey on Biomedical Image Captioning](https://www.aclweb.org/anthology/W19-1803).

> V. Kougia, J. Pavlopoulos and I Androutsopoulos, "A Survey on Biomedical Image Captioning". 
Proceedings of the Workshop on Shortcomings in Vision and Language of the Annual Conference 
of the North American Chapter of the Association for Computational Linguistics (NAACL-HLT 2019), Minneapolis, USA, 2019.

### Install
To install the package locally
```
git clone https://github.com/nlpaueb/dc.git
cd dc
python3 setup.py sdist
pip install dist/dc-0.1.tar.gz 
```

### How to use

```python
from dc.data.downloads import DownloadData
from dc.models.baselines import Baselines
from dc.evaluation.evaluation import Evaluation

downloads = DownloadData()
# downloads the iu_xray dataset in the current directory
downloads.download_iu_xray()
# downloads pubmed2018_w2v_200D word embeddings (https://archive.org/details/pubmed2018_w2v_200D.tar)
downloads.download_bio_embeddings()

baselines = Baselines('iu_xray/train_images.tsv','iu_xray/test_images.tsv','iu_xray/iu_xray_images/','results')
# creates predictions based on the most frequent words used in train captions
baselines.most_frequent_word_in_captions()

# evaluates the predictions
evaluation = Evaluation('iu_xray/test_images.tsv', 'results/most_frequent_word_results.tsv')
evaluation.compute_WMD("pubmed2018_w2v_200D/pubmed2018_w2v_200D.bin")

```
