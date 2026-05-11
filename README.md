# mealpy-lts

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![PyPI - Version](https://img.shields.io/pypi/v/mealpy-lts?style=flat-square)
![PyPI - Implementation](https://img.shields.io/pypi/implementation/mealpy-lts?style=flat-square)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/mealpy-lts?style=flat-square)
![PyPI - Wheel](https://img.shields.io/pypi/wheel/mealpy-lts?style=flat-square)
![GitHub Release Date](https://img.shields.io/github/release-date/ltsim/mealpy-lts.svg?style=flat-square)
![PyPI - Downloads](https://img.shields.io/pypi/dm/mealpy-lts?style=flat-square)

![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/ltsim/mealpy-lts/publish.yml?style=flat-square&logo=pypi&label=Publish)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/ltsim/mealpy-lts/test.yml?style=flat-square&logo=pytest&label=Testing)

This is a maintenance release, a fork of [MEALPY](https://github.com/thieu1995/mealpy), which offers a collection of cutting-edge metaheuristic algorithms. These include nature-inspired algorithms, bio-inspired algorithms, black-box optimization, global search optimizers, iterative learning algorithms, continuous optimization, derivative-free optimization, gradient-free optimization, zero-order optimization, stochastic search optimization, and random search optimization.

All of these methods fall under the category of population-based metaheuristics (PBM), which are among the most popular algorithms in the field of approximate optimization.

For detailed information about the updates in each new version, see the [ChangeLog](/CHANGELOG.md) file.

* **Free software:** MIT license
* **Total algorithms**: 233 (206 official (original, hybrid, variants), 27 developed)
* **Documentation:** https://mealpy.readthedocs.io/en/latest/

## Goals

Our goals are to implement all classical as well as the state-of-the-art nature-inspired algorithms, create a simple interface that helps researchers access optimization algorithms as quickly as possible, and share knowledge of the optimization field with everyone without a fee. What you can do with mealpy:

- Analyse parameters of meta-heuristic algorithms.
- Perform Qualitative and Quantitative Analysis of algorithms.
- Analyse rate of convergence of algorithms.
- Test and Analyse the scalability and the robustness of algorithms.
- Save results in various formats (csv, json, pickle, png, pdf, jpeg)
- Export and import models can also be done with Mealpy.
- **Solve any optimization problem**


## Citation Request

Please include these citations if you plan to use this library:

```bibtex 
@article{van2023mealpy,
  title={MEALPY: An open-source library for latest meta-heuristic algorithms in Python},
  author={Van Thieu, Nguyen and Mirjalili, Seyedali},
  journal={Journal of Systems Architecture},
  year={2023},
  publisher={Elsevier},
  doi={10.1016/j.sysarc.2023.102871}
}

@article{van2023groundwater,
  title={Groundwater level modeling using Augmented Artificial Ecosystem Optimization},
  author={Van Thieu, Nguyen and Barma, Surajit Deb and Van Lam, To and Kisi, Ozgur and Mahesha, Amai},
  journal={Journal of Hydrology},
  volume={617},
  pages={129034},
  year={2023},
  publisher={Elsevier},
  doi={https://doi.org/10.1016/j.jhydrol.2022.129034}
}

@article{ahmed2021comprehensive,
  title={A comprehensive comparison of recent developed meta-heuristic algorithms for streamflow time series forecasting problem},
  author={Ahmed, Ali Najah and Van Lam, To and Hung, Nguyen Duy and Van Thieu, Nguyen and Kisi, Ozgur and El-Shafie, Ahmed},
  journal={Applied Soft Computing},
  volume={105},
  pages={107282},
  year={2021},
  publisher={Elsevier},
  doi={10.1016/j.asoc.2021.107282}
}
```

# Usage

## Installation

* Install the stable (latest) version from [PyPI release](https://pypi.python.org/pypi/mealpy-lts):
```bash
$ pip install mealpy-lts --upgrade
```

* Install the pre-release version directly from the source code:
```bash
$ git clone https://github.com/ltsim/mealpy-lts.git
$ cd mealpy-lts
$ python setup.py install
```

* In case, you want to install the development version from Github:
```bash
$ pip install git+https://github.com/ltsim/mealpy-lts 
```

After installation, check the version to ensure successful installation:

```bash
$ python
>>> import mealpy
>>> mealpy.__version__

>>> print(mealpy.get_all_optimizers())
>>> model = mealpy.get_optimizer_by_name("OriginalWOA")(epoch=100, pop_size=50)
```

## Decision Variables

Before we dive into some examples, let's briefly consider the type of problem you're aiming to solve with MEALPY. 
Understanding your specific problem and its desired solution can help you select the most appropriate approach.

To assist you in choosing the right tools, refer to the table below. It outlines different types of **decision variables** available in MEALPY, 
along with their syntax and common problem applications. This will guide you in defining your search space effectively.

| Class             | Syntax                                                                                                          | Problem Types               |
|-------------------|-----------------------------------------------------------------------------------------------------------------|-----------------------------|
| FloatVar          | `FloatVar(lb=(-10., )*7, ub=(10., )*7, name="delta")`                                                           | Continuous Problem          |
| IntegerVar        | `IntegerVar(lb=(-10., )*7, ub=(10., )*7, name="delta")`                                                         | LP, IP, NLP, QP, MIP        |
| StringVar         | `StringVar(valid_sets=(("auto", "backward", "forward"), ("leaf", "branch", "root")), name="delta")`             | ML, AI-optimize             |
| BinaryVar         | `BinaryVar(n_vars=11, name="delta")`                                                                            | Networks                    |
| BoolVar           | `BoolVar(n_vars=11, name="delta")`                                                                              | ML, AI-optimize             |
| PermutationVar    | `PermutationVar(valid_set=(-10, -4, 10, 6, -2), name="delta")`                                                  | Combinatorial Optimization  |
| CategoricalVar    | `CategoricalVar(valid_sets=(("auto", 2, 3, "backward", True), (0, "tournament", "round-robin")), name="delta")` | MIP,  MILP                  |
| SequenceVar       | `SequenceVar(valid_sets=((1, ), {2, 3}, [3, 5, 1]), return_type=list, name='delta')`                            | Hyper-parameter tuning      |
| TransferBoolVar   | `TransferBoolVar(n_vars=11, name="delta", tf_func="sstf_02")`                                                   | ML, AI-optimize, Feature    |
| TransferBinaryVar | `TransferBinaryVar(n_vars=11, name="delta", tf_func="vstf_04")`                                                 | Networks, Feature Selection |

## Optimizer Classification Table

* Meta-heuristic Categories: ([Based on this article](https://doi.org/10.1016/j.procs.2020.09.075))
    + Evolutionary-based: Algorithms inspired by Darwin's law of natural selection and evolutionary computing principles
    + Swarm-based: Algorithms drawing inspiration from the collective movement and interaction of swarms (e.g., birds, social insects).
    + Physics-based: Algorithms derived from physical laws and phenomena (e.g., Newton's law of universal gravitation, black holes, multiverse theory).
    + Human-based: Algorithms inspired by human interactions and behaviors (e.g., queuing search, teaching-learning processes).
    + Biology-based: Algorithms based on biological creatures or microorganisms.
    + System-based:  Algorithms inspired by ecological systems, immune systems, or network systems.
    + Math-based: Algorithms developed from mathematical forms or laws (e.g., sine-cosine functions).
    + Music-based: Algorithms drawing inspiration from musical instruments or compositions.

* Difficulty - Difficulty Level (Personal Opinion): **Objective observation from author**. Depend on the number of 
  parameters, number of equations, the original ideas, time spend for coding, source lines of code (SLOC).
    + Easy: A few paras, few equations, SLOC very short
    + Medium: more equations than Easy level, SLOC longer than Easy level
    + Hard: Lots of equations, SLOC longer than Medium level, the paper hard to read.
    + Hard* - Very hard: Lots of equations, SLOC too long, the paper is very hard to read.
    
** For newbie, we recommend to read the paper of algorithms which difficulty is "easy" or "medium" difficulty level.

### Warning: Algorithms Suspected of Plagiarism

During our implementation and classification of metaheuristic optimization algorithms, we identified a set of methods that raise 
serious concerns regarding **scientific integrity and originality**. These algorithms are typically published under **different names**, 
but they appear to share:

- The **same core mathematical models**, equations, and update rules.
- Only superficial changes in naming, metaphors, or biological analogies.
- Publications authored by **the same or overlapping research groups**.
- **Heavy criticism** on public academic forums such as [PubPeer](https://pubpeer.com), where many of these papers are flagged for **self-plagiarism**, **redundant publication**, or **lack of novelty**.
- Some of these papers may be **withdrawn or retracted in the future**, as investigations unfold.

For these reasons, we strongly advise the **exclusion** of the following algorithms from scientific benchmarking, 
comparative studies, or any applications unless their originality is transparently validated.

**I have personally implemented these algorithms, which is why I can confidently say that they are nearly identical 
and likely cases of plagiarism. For this reason, I will no longer spend time coding such algorithms in the future. 
This warning is intended to help others avoid using or relying on these methods in their work.**

### Ethical Reminder

Researchers and students are urged to **exercise caution** when referencing or applying the algorithms listed above. 
Using unoriginal or unethical work can compromise the **scientific credibility** of any downstream research and introduce **misleading experimental results**.

> **Check [PubPeer1](https://pubpeer.com/publications/1F5DCE5BC42BF2D77A1B0C281A5295)** and [PubPeer2](https://pubpeer.com/publications/D47357D409AE273F9E03C7CBE30EB7) to 
> find ongoing discussions and critiques from the academic community.

## Examples

### Simple Benchmark Function

MEALPY allows you to define your optimization problem in a couple of ways.

#### 1. Define Problem as a Dictionary

You can quickly define your problem using a Python dictionary. However, this approach is only valid for problems with float decision variables.

```python
from mealpy import FloatVar, SMA
import numpy as np

def objective_function(solution):
    return np.sum(solution**2)

problem = {
    "obj_func": objective_function,
    "bounds": FloatVar(lb=(-100., )*30, ub=(100., )*30),
    "minmax": "min",
    "log_to": "console",
}

## Run the algorithm
model = SMA.OriginalSMA(epoch=100, pop_size=50, pr=0.03)
g_best = model.solve(problem)
print(f"Best solution: {g_best.solution}, Best fitness: {g_best.target.fitness}")
```

#### 2. Define a Custom Problem Class

For more complex scenarios, especially when your decision variables are not exclusively `FloatVar`, 
**we recommend defining a custom class that inherits from the Problem class.**
Let's demonstrate this with a simple "Squared" class.

In the `__init__` method of your custom Problem class (e.g., Squared class), you must set the bounds and minmax attributes of the problem.

+ `bounds`: Defines the search space and the type of decision variables (e.g., `FloatVar`, `IntegerVar`).

+ `minmax`: A string indicating whether the problem is a minimization ("min") or maximization ("max") problem.

After defining the initialization, you must override the abstract method `obj_func()`. This method is the core of your problem definition:

+ It takes a single parameter: solution (the encoded solution vector generated by the optimizer).

+ It must return the objective function value (or fitness) for the given solution.

The resulting code structure for a custom problem class would look similar to the snippet below. 
You can include any additional parameters you need in your custom class (like '`data`' or '`name`' in this example).


```python
from mealpy import Problem, FloatVar, BBO 
import numpy as np

# Our custom problem class
class Squared(Problem):
    def __init__(self, bounds=None, minmax="min", data=None, **kwargs):
        super().__init__(bounds, minmax, **kwargs)
        self.data = data     # This is additional variable use for passing data to objective function

    def obj_func(self, solution):
        return np.sum(solution ** 2)

    
## Now, we define an algorithm, and pass an instance of our *Squared* class as the problem argument. 
bound = FloatVar(lb=(-10., )*20, ub=(10., )*20, name="my_var")      # The `name` of variable is important when decoding.
problem = Squared(bounds=bound, minmax="min", name="Squared", data="Amazing")
model = BBO.OriginalBBO(epoch=100, pop_size=20)
g_best = model.solve(problem)

## Show some attributes
print(g_best.solution)
print(g_best.target.fitness)
print(g_best.target.objectives)
print(g_best)
print(model.get_parameters())
print(model.get_name())
print(model.get_attributes()["g_best"])
print(model.problem.get_name())
print(model.problem.n_dims)
print(model.problem.bounds)
print(model.problem.lb)
print(model.problem.ub)
```

We provide many examples for complicated applications that can use Mealpy to solve.

---

* Maintained by: [LTSIM](mailto:tsim@cucei.udg.mx) @ 2026
* Developed by: [Thieu](mailto:nguyenthieu2102@gmail.com?Subject=Opfunu_QUESTIONS) @ 2023