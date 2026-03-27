# Brechas digitales en humanidades
### Demandas del mercado vs. lo que enseñan las universidades peruanas

**Autor:** Wilman Ricardo Pacheco Quispe
**Año:** 2026

---

## Descripción

Este proyecto analiza la brecha entre las competencias digitales que demandan las ofertas laborales peruanas y las que declaran formar los perfiles de egreso de carreras de humanidades y ciencias sociales. El análisis combina tres métodos de NLP sobre un corpus de 100 documentos en español (50 ofertas laborales + 50 perfiles de egreso de universidades con licenciamiento SUNEDU vigente).

**Pregunta de investigación:** ¿Qué competencias digitales predominan en las ofertas laborales dirigidas a egresados de humanidades y ciencias sociales, y en qué medida están presentes en los perfiles de egreso de las universidades peruanas?

---

## Métodos

| Etapa | Método | Herramienta |
|---|---|---|
| 1 | Web scraping de ofertas laborales | Playwright (Bumeran + LinkedIn) |
| 2 | Preprocesamiento de texto | spaCy `es_core_news_md` |
| 3 | Análisis léxico | TF-IDF + similitud coseno (scikit-learn) |
| 4 | Extracción de competencias digitales | Claude Opus 4.6 (Anthropic API) |
| 5 | Validación de extracción | Kappa de Cohen (κ = 0.636) |
| 6 | Análisis semántico | Embeddings `text-embedding-3-large` (OpenAI) |

---

## Hallazgos principales

- La similitud léxica (TF-IDF) entre ofertas y perfiles es de **0.04** en promedio: ambos grupos operan en registros completamente distintos.
- Los embeddings semánticos elevan esa similitud a **0.366**, lo que indica que parte de la brecha es aparente, pero el desajuste de contenido persiste.
- Las competencias digitales que demanda el mercado son operacionales: Excel, Google Drive, T-Registro, PLAME, sistemas de nómina. Estas competencias están **prácticamente ausentes** en los perfiles de egreso.
- **Humanidades Digitales** es la única carrera con alineación sistemática con el mercado (similitud promedio: 0.425). En el extremo opuesto, Filosofía, Literatura y Ciencias de la Información presentan los mayores desacoples.
- La brecha no es una peculiaridad peruana: el BID (2023) reporta que el 38% de trabajadores en empresas líderes en Perú carece de competencias digitales necesarias, y UNESCO IESALC (2024) documenta que solo el 45% de universidades latinoamericanas tiene lineamientos formales en competencias digitales, frente al 70% en Europa y América del Norte.

---

## Estructura del repositorio

```
.
├── code.ipynb                 # Notebook principal con todo el análisis
├── corpus.xlsx                # 50 perfiles de egreso (universidades peruanas)
├── ofertas_laborales.xlsx     # Corpus consolidado de ofertas (Bumeran + LinkedIn)
├── ofertas_bumeran.xlsx       # Ofertas scrapeadas de Bumeran
├── ofertas_linkedin.xlsx      # Ofertas scrapeadas de LinkedIn
├── resultados_llm.xlsx        # Competencias digitales extraídas por el LLM
└── README.md
```

---

## Requisitos

```bash
pip install playwright spacy anthropic openai scikit-learn pandas numpy matplotlib python-dotenv
python -m spacy download es_core_news_md
playwright install chromium
```

Configura un archivo `.env` en la raíz del proyecto con:

```
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
```

---

## Referencias

- Alibasic, A., Upadhyay, H., Simsekler, M. C. E., Kurfess, T., Woon, W. L., & Omar, M. A. (2022). Evaluation of the trends in jobs and skill-sets using data analytics: a case study. *Journal of Big Data*, 9(1), 32. https://doi.org/10.1186/s40537-022-00576-5
- BID. (2023). *Estudio de Talento Digital en el Perú 2023: La demanda insatisfecha de talento digital*. https://publications.iadb.org
- CEPAL. (2024). *Educación y desarrollo de competencias digitales en América Latina y el Caribe*. https://repositorio.cepal.org
- Corradi, B., McGinn, N., & Maldonado, K. (2024). Factors contributing to the (un)fulfilment of employment aspirations of recent Chilean university graduates. *Journal of Education and Work*, 37(1–4), 198–215. https://doi.org/10.1080/13639080.2024.2383560
- Díaz-Becerra, O. A., Cuyate Reque, P. J., Beltrán Portilla, F. M., & Campos Díaz, R. C. (2025). Identificación de competencias genéricas y específicas en los perfiles de egresados de universidades peruanas. *Proyecciones. Revista de Contabilidad y Finanzas*, 21. https://doi.org/10.24215/26185474e041
- Ferreira, A., Gómez, W., & Grünewald, I. (2025). Natural language processing techniques to identify work profiles from online job postings. En T. Guarda et al. (Eds.), *ARTIIS 2024. Communications in Computer and Information Science*, vol. 2345. Springer. https://doi.org/10.1007/978-3-031-83207-9_28
- Grimmer, J., Roberts, M. E., & Stewart, B. M. (2022). *Text as data: A new framework for machine learning and the social sciences*. Princeton University Press.
- Hou, Y., & Huang, J. (2025). Natural language processing for social science research: A comprehensive review. *Social Science Computer Review*. https://doi.org/10.1177/2057150X241306780
- LATAM Revista. (2024). Tendencias y reformas curriculares en la educación superior latinoamericana (2018–2023). *LATAM*, Redilat.
- UNESCO IESALC. (2024). *Transforming the digital landscape of higher education in Latin America and the Caribbean*. https://unesdoc.unesco.org
- World Economic Forum. (2025). *Future of Jobs Report 2025*. https://www.weforum.org/reports/the-future-of-jobs-report-2025
