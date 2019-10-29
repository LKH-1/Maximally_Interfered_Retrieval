## Online Continual Learning with Maximally Interfered Retrieval (NeurIPS 2019)

Controlled sampling of memories for replay: retrieving the samples which are most interfered, i.e. whose prediction will be most negatively impacted by the foreseen parameters update. </br>

* [paper](https://arxiv.org/abs/1908.04742)
* [summary](https://www.shortscience.org/paper?bibtexKey=journals/corr/1908.04742)
* [video](https://www.youtube.com/watch?v=wfb9UV_n8jg)

## (key) Requirements 
- Python 3.6
- Pytorch 1.1.0

`pip install -r requirements.txt`

## Structure

    ├── Scripts 
        ├── ER_experiments.sh                # reproduces Experience Replay (ER) results        
        ├── ER_experiments_miniimagenet.sh   # reproduces ER results on MiniImagenet
        ├── gen_hparam_search.py             # Hyperparameter search for Generative Replay (GEN) 
        ├── gen_reproduce.py                 # reproduces GEN results 
        ├── hybrid_reproduce.sh              # reproduces Hybrid Replay (AE) results
    ├── VAE           
        ├── ....            # files for the VAE used in GEN
    ├── buffer.py           # Basic buffer implementation for ER and AE
    ├── data.py             # DataLoaders
    ├── er_main.py          # main file for ER
    ├── gen_main.py         # main file for GEN    
    ├── hybrid_main.py      # main file for AE
    ├── mir.py              # retrieval functions for ER, GEN and AE    
    ├── model.py            # defines the classifiers and the AutoEncoder in AE
    ├── utils.py

## Running Experiments

* ER = Experience Replay baseline
* ER-MIR = Experience Replay + Maximally Interfered Retrieval
* GEN = Generative Replay baseline
* GEN-MIR = Generative Replay + Maximally Interfered Retrieval
* AE = Hybrid Replay baseline
* AE-MIR = Hybrid Replay + Maximally Interfered Retrieval

#### Experience Replay

ER baseline example:  </br>

`python er_main.py --method rand_replay --dataset split_cifar10 --mem_size 50`

ER-MIR example:  </br>

`python er_main.py --method mir_replay --dataset split_cifar10 --mem_size 50`

Reproduce:  </br>

`sh Scripts/ER_experiments.sh`

#### Generative Replay

GEN baseline example:  </br>

`python gen_main.py --method rand_gen --gen_method rand_gen --samples_per_task 1000`

GEN-MIR (MIR only on the classifier):  </br>

`python gen_main.py --method mir_gen --gen_method rand_gen --samples_per_task 1000`

GEN-MIR (MIR only on the generator):  </br>

`python gen_main.py --method rand_gen --gen_method mir_gen --samples_per_task 1000`

GEN-MIR:  </br>

`python gen_main.py --method mir_gen --gen_method mir_gen --samples_per_task 1000`

Hyper-parameter search:  </br>

`python Scripts/gen_hparam_search.py`

Reproduce:  </br>

`python Scripts/gen_reproduce.py`

#### Hybrid Replay

AE baseline example:  </br>

`python hybrid_main.py --max_loss  --mem_size 1000  --buffer_batch_size 100 `

AE-MIR example:  </br>

`python hybrid_main.py --mem_size 1000  --buffer_batch_size 100 `

Reproduce:  </br>

`sh Scripts/hybrid_reproduce.sh`

 
## Logging


## Acknowledgements 
We would like to thank authors of the following repositories (from which we borrowed code) for making the code public. </br>
* https://github.com/riannevdberg/sylvester-flows



## Cite
```
@article{Aljundi2019OnlineCL,
  title={Online Continual Learning with Maximally Interfered Retrieval},
  author={Rahaf Aljundi and Lucas Caccia and Eugene Belilovsky and Massimo Caccia and Min Lin and Laurent Charlin and Tinne Tuytelaars},
  journal={ArXiv},
  year={2019},
  volume={abs/1908.04742}
}
```




