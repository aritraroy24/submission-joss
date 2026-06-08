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

ComProScanner is an open-source Python package that automates the extraction of composition--property data from materials science literature, operating as a fully end-to-end pipeline from literature search to structured database construction without human intervention, provided publisher Text and Data Mining (TDM) API keys are supplied. Building on the previously introduced ComProScanner framework [@roy2026comproscanner], this release extends it with native vision language model (VLM)-based figure extraction, enabling the recovery of composition-property pairs from scientific charts and plots embedded in journal articles. giving users the flexibility to configure any LiteLLM-compatible model for both text extraction and figure interpretation.

# Statement of need

A substantial fraction of quantitative composition-property data such as piezoelectric coefficients in the materials science literature is reported exclusively in graphical form. For example, bar charts, scatter plots and line graphs encoding piezoelectric coefficients, dielectric constants or mechanical responses across doped compositions are ubiquitous in experimental publications, yet the numerical values they contain are frequently absent from article text or supplementary tables. Existing extraction frameworks, including the prior version of ComProScanner, are limited to textual and tabular content and are therefore systematically blind to this class of information. Specialised plot digitisation tools such as Plot2Spectra [@jiang2022plot2spectra], MatGD [@lee2024matgd] and LineEX [@shivasankaran2023lineex] have demonstrated that automated numerical extraction from figures is feasible, but they operate as standalone digitisers requiring figure-type-specific engineering and are not integrated into any end-to-end literature mining pipeline. The VLM extension presented here addresses this gap by coupling figure extraction natively with ComProScanner's existing publisher API access, multi-agent orchestration, and structured output schema, enabling researchers to build composition-property databases that capture data from text, tables and figures within a single automated workflow.

# State of the field

Automated extraction of materials data from scientific literature has progressed considerably over the past decade, from rule-based and named entity recognition approaches [@swain2016chemdataextractor],[@mavracic2021chemdataextractor2] to LLM-based pipelines employing prompt engineering [@dagdelen2024structured],[@polak2024chatextract] and multi-agent orchestration [@ansari2024eunomia],[@ghosh2026automated]. However, virtually all existing frameworks operate exclusively on text and tables. The closest multimodal comparator in the materials domain is nanoMINER [@odobesku2025nanominer], which combines YOLO-based visual detection with GPT-4o for nanomaterials information extraction; however, it requires manual article provision and does not offer automated publisher access. On the chart understanding side, models such as DePlot [@liu2023deplot] and MatCha [@liu2023matcha] have demonstrated strong zero-shot performance on general chart comprehension tasks, whilst Zheng et al. [@zheng2024reticular] and PlotExtract [@plotextract2025] have shown that VLMs can extract quantitative data from chemistry and materials figures with high accuracy. ComProScanner is the first framework to integrate VLM-based figure extraction as a native, configurable component of a fully automated, publisher-integrated, materials-specific composition-property extraction pipeline. The updated overall workflow and the modified multi-agent extraction flow are illustrated in Figure [@fig-brass].
![(a) Overall workflow diagram of ComProScanner framework incorporating the GraphExtractorTool and EquationTool. (b) Flow diagram of ComProScanner framework’s information extraction process
incorporating the image-aware RAGTool, GraphExtractorTool, EquationTool and Material-ParserTool. The
detailed descriptions for other components can be found in the original ComProScanner paper](img/portal.png){#fig-bruss width=95%}

# Software design

The VLM extension introduces two principal components into the existing ComProScanner architecture. The first is `FigureExtractor`, a shared utility that identifies figures whose captions match user-specified keywords and saves them as JPEG images to a DOI-keyed directory, handling JPEG/JPG, as well as transparent PNG and animated GIF formats. The second, but more significant component is `GraphExtractorTool`, a CrewAI BaseTool that, given a DOI, reads all previously saved figures and submits them to a configurable VLM with a structured prompt designed to recover composition-property value pairs, returning results in the standard ComProScanner JSON schema. The tool is invoked by the Composition-Property Data Extractor agent within the existing five-agent CrewAI workflow. An image-aware fallback has additionally been added to the Materials Data Identifier agent: if the initial text-based RAG step returns a negative result, the agent queries available figures via VLM before deciding whether to proceed with full extraction, preventing articles with graph-only data from being discarded prematurely.

More information on experiment development and contribution to the expfactory tools, containers, or library is provided at the Experiment Factory <a href="https://expfactory.github.io/expfactory/" target="_blank">official documentation</a>. This is an Open Source project, and so <a href="https://www.github.com/expfactory/expfactory/issues" target="_blank">feedback and contributions</a> are encouraged and welcome.

# References
