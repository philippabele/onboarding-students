# LaTeX documentation

- create a .\docs folder in your project repository
- set up the GitHub Actions for LaTeX configuration

<br />

# GitHub Actions for LaTeX

To simplify the workflow for writing and reviewing the LaTeX documentation a GitHub Action is used to compile the documentation into a PDF file.

The Action is configured in [`.github/workflows/compile-latex.yml`](../.github/workflows/compile-latex.yml).

## Trigger

The [trigger](https://docs.github.com/en/actions/using-workflows/triggering-a-workflow) defines when the workflows should run and can be set with the `on`. For this documentation the trigger is set to:

```yml
on:
  pull_request:
    branches:
      - main
    paths:
      - 'docs/**'
```

With this configuration the Action is run on every PR creation/update that includes changes inside of the `docs` folder and that has the target branch set to `main`.

## Jobs

A workflow/action contains one ore more [jobs](https://docs.github.com/en/actions/using-jobs/using-jobs-in-a-workflow) that execute the logic of the workflow/action. By default, all jobs run in parallel. For our use case we only use one job (`compile`) that is defined as:

```yml
jobs:
  compile:
    runs-on: ubuntu-latest
    env:
      working_directory: docs
      pdf_name: INF19B_Rickert_2858031_T3101
    steps:
    ...
```

This configuration defines that the job should run on the ubuntu (linux) operating system. It also sets two environment variables that are later being used:

- `working_directory`: Path to the LaTeX documentation files
- `pdf_name`: Name of the output PDF

### Steps

The actual implementation of our workflow/action is defined in the [steps](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idsteps) of a job. They are e.g. bash commands that should be executed.

In order to compile the LaTeX documentation the following steps are needed:

```yml
steps:
  - name: Checkout Git repository
    uses: actions/checkout@v2
  - name: Compile LaTeX document
    uses: xu-cheng/latex-action@v2
    with:
      working_directory: ${{ env.working_directory }}
      root_file: main.tex
  - name: Rename main.pdf
    run: |
      mv "$working_directory/main.pdf" "$pdf_name.pdf"
  - name: Upload pdf artifact
    uses: actions/upload-artifact@v2
    with:
      name: ${{ env.pdf_name }}
      path: ${{ env.pdf_name }}.pdf
      if-no-files-found: error
```

1. First this GitHub repository is checked out so that the Job has access to all
   files.
2. Then the pre-build Action `xu-cheng/latex-action@v2` is used to compile the LaTeX code into a PDF. As parameters we pass the `working_directory` (path to the `.tex` files) which in our case is `docs` and the name of the main LaTeX file which is `main.tex`
3. After the second step is complete a `main.pdf` will be generated which is our compiled documentation. To give it a better suited name it will be renamed the name that was defined in the jobs `pdf_name` environment variable
4. Until now the PDF only exists in the current workflow/action run so we cannot directly access it. To change this, the last step uploads the PDF file to the workflow/action run

## Access the compiled PDF

To access the compiled PDF file go to the `Actions` tab in GitHub and click on the desired workflow/action run. You wil see the PDF at the bottom in the `Artifacts` section.
