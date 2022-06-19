# Workflow Templates
Templates of GitHub Workflows for different programming languages. Place the workflow file you want to use in ```.github/workflows/```.

Want to **contribute**? Open up a pull request! My goal is to have as many languages here as possible so any contribution is welcome.

### List of available templates

| Language |
| -------- |
| [Python](workflows/python.yml) |
| [Golang](workflows/golang.yml) |
| [Node / React](workflows/node.yml) |
| [CMake / C++](workflows/cmake.yml) |
| [Rust](workflows/rust.yml) |

### Base layout

Base workflow file for every programming language:
```yml
name: Name of workflow
# when to run the workflow
on:
  push:
    ...
  pull_request:
# instructions the workflow will perform
jobs:
  build:
    # environment to run on
    runs-on: ubuntu-latest
    # steps to perform
    steps:
    - uses: actions/checkout@v2

    - name: Set up language
      ...

    - name: Install dependencies
      working-directory: ./path/to/folder
      ...

    - name: Build program
      working-directory: ./path/to/folder
      ...

    - name: Run tests
      working-directory: ./path/to/folder
      ...

    - name: Syntax checker
      working-directory: ./path/to/folder
      ...
```

Under the section that decides when to run the workflow you can decide on specific paths. Below you can see an example where the workflow will only run when changes is pushed to the ```path/to/file/main.py``` file or when anything changes in the ```path/to/folder/``` directory. This limits the amount of time the workflow is run and helps with reducing the time it takes to get the results. It is recommended to add the workflow file to this list as it triggers the workflow to run on any changes you apply to it, testing the workflow instantly.

Pull requests aren't set to any specific path since it's recommended to run every workflow before merging the branch with main. This reduces the likelihood of mistakes being pushed to the main branch.

```yml
on:
  push:
    paths:
    - 'path/to/file/main.py'
    - 'path/to/folder/**'
  pull_request:
```

Under the section that is named ```set up language``` you decide the programming language that is relevant for the workflow. Below you have an example with Python. The Python version needs to be changed to whats relevant to your needs.

```yml
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9.10'
```

The rest of the steps are all different depending on the language. The step running the tests might not be relevant for each workflow so might not be present. You can change the path in the working directory to ```.``` if you wish to work in the root directory.

