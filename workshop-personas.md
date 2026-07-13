# Workshop Personas

**Generated:** 2026-07-10
**Domain(s):** NASA earth science, remote sensing, cryosphere, hydrosphere, atmosphere, data science, data access, software engineering, geoscience, generative AI, machine learning
**Career stages:** graduate students, postdocs, research staff, faculty, industry partners, technicians, software engineers, data managers
**Technical background:** intermediate to advanced Python users, some experience using generative AI for scientific research, experience working with NASA earth datasets
**Institutional context:** NASA earth sciences, NASA data centers

---

## Amara Osei

**Field:** Cryosphere science / sea ice dynamics
**Career stage:** PhD student (2nd year)
**Python comfort level:** comfortable with NumPy, xarray, and Matplotlib for analyzing NetCDF files; can adapt existing scripts but struggles when building modular workflows from scratch; relies on Stack Overflow and example notebooks from NSIDC tutorials
**Current AI tool usage:** uses ChatGPT to explain error messages and generate boilerplate pandas operations; tried GitHub Copilot for a semester but found suggestions unreliable for geospatial code and stopped using it
**Motivation:** I spend most of my time wrestling with NSIDC datasets just to get them into a usable format before any real analysis begins. I want to see if AI tools can accelerate that preprocessing pipeline so I have more time for actual science.
**Primary concern:** worried that AI-generated code will silently mishandle coordinate reference systems or polar stereographic projections in ways I won't catch until my results look wrong
**What success looks like:** can use Claude Code to write and debug an xarray-based ingestion pipeline for NSIDC sea ice concentration data without spending a half-day on data wrangling before any analysis begins

---

## Priya Nair

**Field:** Atmospheric science / satellite remote sensing (MODIS and VIIRS aerosol retrievals)
**Career stage:** research scientist (NASA GSFC, 6 years post-PhD)
**Python comfort level:** advanced — writes reusable libraries, parallelizes processing with Dask on cloud infrastructure, comfortable with Earthdata Cloud S3 access and STAC catalog queries; occasionally contributes to open-source geospatial tools
**Current AI tool usage:** regularly uses Claude and GitHub Copilot for code review, documentation generation, and refactoring legacy IDL-to-Python conversions; skeptical of AI for scientific reasoning but actively uses it for boilerplate and test scaffolding
**Motivation:** I maintain a pipeline that ingests Level-2 aerosol retrievals from multiple sensors across a 20-year archive and feeds downstream users who publish from it. I want to understand how AI-assisted code generation can help me modernize those legacy scripts without introducing regressions I'll only discover after a product version ships.
**Primary concern:** unclear on NASA data center policy about what pre-publication data can be sent to external LLM APIs, and worried about accidentally violating data sharing agreements when pasting code snippets that embed file paths or metadata
**What success looks like:** can articulate a clear policy for which parts of a long-running NASA data pipeline are safe to refactor with AI assistance, and has a verification checklist for confirming AI-generated changes don't alter scientific output values

---

## Jordan Whitfield

**Field:** Applied machine learning for Earth observation / cloud-native geospatial platforms
**Career stage:** senior software engineer (industry partner, commercial remote sensing startup)
**Python comfort level:** expert — builds production ML pipelines with PyTorch and scikit-learn applied to satellite imagery, manages CI/CD workflows and AWS infrastructure; writes automated tests as a default practice
**Current AI tool usage:** uses Cursor and Claude Code as daily pair-programming tools; has integrated AI code review into pull request workflows; occasionally frustrated when AI tools don't recognize NASA-specific APIs, Earthdata authentication patterns, or HDF-EOS file structures
**Motivation:** I build tools that NASA data center users and researchers consume, and I want a clearer picture of where AI assistance actually breaks down in earth science workflows so I can improve documentation, onboarding, and API design for those users.
**Primary concern:** concerned that AI models trained on generic Python and generic geospatial code won't understand domain-specific edge cases like polar projection discontinuities, HDF-EOS group hierarchies, or Earthdata token-based authentication flows — and that researchers won't know when to distrust AI output in those contexts
**What success looks like:** leaves the workshop with at least three documented failure modes in AI-assisted NASA data workflows that can directly inform the next product sprint

---

## Elena Vasquez

**Field:** Hydrology / land surface water dynamics (GRACE-FO terrestrial water storage, SWOT river discharge)
**Career stage:** postdoctoral researcher (18 months post-PhD)
**Python comfort level:** solid scripting ability — uses pandas, geopandas, and rasterio for watershed-scale analysis; prefers Jupyter notebooks over standalone scripts; avoids writing classes or functions and tends to duplicate code blocks across notebooks
**Current AI tool usage:** uses Claude regularly for grant writing and paper editing; only recently started asking it to generate Python code; finds the experience inconsistent — sometimes the first suggestion works, but errors in follow-up prompts are hard to diagnose because she's unsure what went wrong
**Motivation:** My PhD used IDL for all data processing, and the overhead of relearning syntax while simultaneously running a new research project is slowing me down significantly. I want to know how reliably AI can handle that translation work so I can spend cognitive energy on hydrology rather than Python idioms.
**Primary concern:** worried about becoming dependent on AI-generated code she doesn't fully understand, which could undermine her credibility when presenting methodology to dissertation advisors or co-authors who ask detailed questions about implementation choices
**What success looks like:** can use an AI tool to translate a 200-line IDL script for computing GRACE-FO terrestrial water storage anomalies into working Python, and can verify the output matches the original results well enough to defend the translation in a methods section
