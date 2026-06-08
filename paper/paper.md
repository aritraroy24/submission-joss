---
title: "Beyond Text and Tables: Vision-Language Model Integration in ComProScanner for Extracting Materials Data from Scientific Figures with High Accuracy"
tags:
  - Python
  - information retrieval
  - artificial intelligence
  - large language models
  - vision language models
  - multimodal data extraction
  - multi-agent framework
authors:
  - name: Aritra Roy
    orcid: 0000-0003-0243-9124
    affiliation: "1,2"
  - name: Enrico Grisan
    orcid: 0000-0002-7365-5652
    affiliation: 3
  - name: Chiara Gattinoni
    orcid: 0000-0002-3376-6374
    affiliation: 4
  - name: John Buckeridge
    orcid: 0000-0002-2537-5082
    affiliation: "1,2"
affiliations:
  - name: Energy, Materials and Environment Research Centre, London South Bank University, London SE1 0AA, UK.
    index: 1
    ror: 02vwnat91
  - name: School of Engineering and Design, London South Bank University, London SE1 0AA, UK.
    index: 2
    ror: 02vwnat91
  - name: Bioscience and Bioengineering Research Centre, London South Bank University, London SE1 0AA, UK.
    index: 3
    ror: 02vwnat91
  - name: Department of Physics, Kings College London, London WC2R 2LS, UK.
    index: 4
    ror: 0220mzb33
date: 07 June 2026
bibliography: paper.bib
---

# Summary

ComProScanner is an open-source Python package that automates the extraction of composition--property data from materials science literature, operating as a fully end-to-end pipeline from literature search to structured database construction without human intervention, provided publisher Text and Data Mining (TDM) API keys are supplied. Building on the previously introduced ComProScanner framework [@Roy:2026], this release extends it with native vision language model (VLM)-based figure extraction, enabling the recovery of composition-property pairs from scientific charts and plots embedded in journal articles. giving users the flexibility to configure any LiteLLM-compatible model for both text extraction and figure interpretation.

# Statement of need

A substantial fraction of quantitative composition-property data such as piezoelectric coefficients in the materials science literature is reported exclusively in graphical form. For example, bar charts, scatter plots and line graphs encoding piezoelectric coefficients, dielectric constants or mechanical responses across doped compositions are ubiquitous in experimental publications, yet the numerical values they contain are frequently absent from article text or supplementary tables. Existing extraction frameworks, including the prior version of ComProScanner, are limited to textual and tabular content and are therefore systematically blind to this class of information. Specialised plot digitisation tools such as Plot2Spectra [@Jiang:2022], MatGD [@Lee:2024] and LineEX [@P:2023] have demonstrated that automated numerical extraction from figures is feasible, but they operate as standalone digitisers requiring figure-type-specific engineering and are not integrated into any end-to-end literature mining pipeline. The VLM extension presented here addresses this gap by coupling figure extraction natively with ComProScanner's existing publisher API access, multi-agent orchestration, and structured output schema, enabling researchers to build composition-property databases that capture data from text, tables and figures within a single automated workflow.

# State of the field

Automated extraction of materials data from scientific literature has progressed considerably over the past decade, from rule-based and named entity recognition approaches [@Swain:2016,@Mavracic:2021] to LLM-based pipelines employing prompt engineering\cite{Dagdelen:2024,Polak:2024} and multi-agent orchestration\cite{Ansari:2024,Ghosh:2026}.

# Experiment Container Usage

Once a container is generated and it's unique identifier and image layers served in a registry like Docker Hub, it can be cited in a paper with confidence that others can run and reproduce the work simply by using it.

More information on experiment development and contribution to the expfactory tools, containers, or library is provided at the Experiment Factory <a href="https://expfactory.github.io/expfactory/" target="_blank">official documentation</a>. This is an Open Source project, and so <a href="https://www.github.com/expfactory/expfactory/issues" target="_blank">feedback and contributions</a> are encouraged and welcome.

# References
