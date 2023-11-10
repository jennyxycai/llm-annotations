# llm-annotations

### Datasets
| Dataset  | Entities |
| ------------- | ------------- |
| BC5DR-chem  | chemicals |
| BC5DR-disease  | disease  |
| NCBI-disease  | disease  |
| BC2GM  | genes |
| JNLPBA | proteins |


All of these Biomedical NER datasets use the BIO scheme for encoding entity annotations as token tags. Labels B, I, and O are in the 2nd column of tsv files.<br>
B: begin (beginning of the entity)<br>
I: inside (middle of the entity)<br>
O: outside of named entities (e.g. label O in BC5DR-chem dataset means token isn't a chemical; is equivalent to O-Chemical tag written in the format &lt;B/I/O&gt;-&lt;Entity&gt;)

Source: <i>B. Overview of Experimental Setup</i> of <a href="https://arxiv.org/pdf/2011.06315v1.pdf">article</a>
