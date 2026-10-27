from pathlib import Path

original = Path("/mnt/data/Pasted text(20261027-050425).txt")
text = original.read_text(encoding="utf-8")

# Preserve the existing photo, project cards, radar graphics, contribution calendar,
# animated snake, stats, certifications, links, and overall README structure.
replacements = [
    (
        "https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=26&duration=2600&pause=900&color=E91E63&center=true&vCenter=true&width=650&lines=Deekshita+Rajesh;Data+Analyst;GenAI+%26+AI%2FML+Engineer;Data+Engineer;Software+Engineer;01000100+01000001+01010100+01000001",
        "https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=26&duration=2600&pause=900&color=E91E63&center=true&vCenter=true&width=700&lines=Deekshita+Rajesh;Software+Development+Engineer;Data+Structures+%26+Algorithms;Backend+%26+Distributed+Systems;System+Design+%26+Cloud"
    ),
    (
        "## `~/` whoami\n\n```console\n$ whoami\nDeekshita Rajesh\n\n$ focus --current\nSoftware Engineering\n\n$ objective\nTurn data into decisions, intelligent systems, and production-ready software.\n```\n\nI build end-to-end systems that connect **data, analytics, machine learning and software engineering**.\nMy work spans the full path from raw data and business questions to analytical models, APIs, AI workflows and deployable applications.\n\n> **Analyze the data. Engineer the system. Automate the decision.**",
        "## `~/` whoami\n\n```console\n$ whoami\nDeekshita Rajesh\n\n$ role --focus\nSoftware Development Engineer\n\n$ core_skills\nData Structures & Algorithms | OOP | Backend | System Design\n\n$ objective\nDesign, build, test, and scale reliable software systems.\n```\n\nI focus on **problem-solving, software development, backend engineering, and scalable system design**. I enjoy turning complex requirements into efficient, maintainable, and reliable software.\n\n> **Think in algorithms. Engineer for reliability. Build for scale.**"
    ),
    (
        "https://skillicons.dev/icons?i=python,postgres,mongodb,pytorch,tensorflow,fastapi,docker,git,github,react,nextjs,typescript,html,css&perline=14",
        "https://skillicons.dev/icons?i=python,java,cpp,postgres,mysql,mongodb,spring,fastapi,aws,docker,git,github,linux&perline=13"
    ),
    (
        "<code>Python</code> · <code>Java</code> · <code>SQL</code>",
        "<code>Python</code> · <code>Java</code> · <code>C++</code> · <code>SQL</code>"
    ),
    (
        "<code>REST APIs</code> · <code>Microservices</code><br>\n      <code>Spring Boot</code> · <code>Authentication</code><br>\n      <code>Error Handling</code>",
        "<code>REST APIs</code> · <code>Spring Boot</code><br>\n      <code>API Design</code> · <code>Authentication</code><br>\n      <code>Error Handling</code> · <code>Microservices</code>"
    ),
    (
        "<code>Amazon DynamoDB</code> · <code>PostgreSQL</code><br>\n      <code>MySQL</code> · <code>Amazon RDS</code><br>\n      <code>Amazon ElastiCache</code>",
        "<code>PostgreSQL</code> · <code>MySQL</code><br>\n      <code>Amazon DynamoDB</code> · <code>Amazon RDS</code><br>\n      <code>Indexing</code> · <code>Query Optimization</code>"
    ),
    (
        "<code>Git</code> · <code>GitHub</code> · <code>Linux</code><br>\n      <code>Docker</code> · <code>CI/CD</code><br>\n      <code>Unit Testing</code>",
        "<code>Git</code> · <code>GitHub</code> · <code>Linux</code><br>\n      <code>Docker</code> · <code>CI/CD</code><br>\n      <code>Unit Testing</code> · <code>Debugging</code>"
    ),
    (
        "<code>Operating Systems</code> · <code>Computer Networks</code> ·\n      <code>DBMS</code> · <code>Concurrency</code> ·\n      <code>Multithreading</code> · <code>Object-Oriented Design</code> ·\n      <code>Scalability</code>",
        "<code>Operating Systems</code> · <code>Computer Networks</code> ·\n      <code>DBMS</code> · <code>OOP</code> ·\n      <code>Concurrency</code> · <code>Multithreading</code> ·\n      <code>Object-Oriented Design</code> · <code>Scalability</code>"
    ),
    (
        "## `~/` engineering loop\n\n```text\n                         BUSINESS / USER PROBLEM\n                                   │\n                                   ▼\n                            DEFINE THE QUESTION\n                                   │\n                                   ▼\n                              RAW DATA + CONTEXT\n                                   │\n                     ┌─────────────┴─────────────┐\n                     ▼                           ▼\n              CLEAN / VALIDATE              ANALYZE / MODEL\n                     │                           │\n                     └─────────────┬─────────────┘\n                                   ▼\n                         INSIGHT / INTELLIGENCE\n                                   │\n                                   ▼\n                         API / DASHBOARD / APP\n                                   │\n                                   ▼\n                              DEPLOY + OBSERVE\n                                   │\n                                   ▼\n                              MEASURE + ITERATE\n```\n\nThe goal is not to build isolated notebooks or isolated AI demos. It is to build **reproducible systems that answer real questions and produce usable outcomes**.",
        "## `~/` engineering loop\n\n```text\n                         USER / SYSTEM REQUIREMENT\n                                   │\n                                   ▼\n                         PROBLEM DECOMPOSITION\n                                   │\n                                   ▼\n                         DATA STRUCTURES & ALGORITHMS\n                                   │\n                                   ▼\n                           DESIGN & ARCHITECTURE\n                                   │\n                                   ▼\n                              IMPLEMENTATION\n                                   │\n                                   ▼\n                         UNIT + INTEGRATION TESTS\n                                   │\n                                   ▼\n                          CODE REVIEW + DEBUGGING\n                                   │\n                                   ▼\n                           CI/CD + DEPLOYMENT\n                                   │\n                                   ▼\n                         MONITOR + OPTIMIZE + SCALE\n```\n\nI aim to build **maintainable, tested, and reliable software**—from understanding requirements and choosing the right data structures to deployment, monitoring, and iterative improvement."
    ),
    (
        "| **[NexoraAgri](https://github.com/deekshitaa1/NexoraAgri)** | AI Engineering · ML | Data validation → temporal features → classification + regression → explainability → decision engine |\n| **[OmniRAG](https://github.com/deekshitaa1/OmniRAG)** | AI Engineering · Data Engineering | Document ingestion → extraction → chunking → PostgreSQL → vector retrieval → RAG |\n| **[CodeSync](https://github.com/deekshitaa1/CodeSync)** | Software Engineering | Frontend/backend integration → APIs → real-time collaboration → maintainable application architecture |",
        "| **[CodeSync](https://github.com/deekshitaa1/CodeSync)** | Software Engineering | Frontend/backend integration → API design → real-time collaboration → maintainable application architecture |\n| **[OmniRAG](https://github.com/deekshitaa1/OmniRAG)** | Backend · Data Systems | Document ingestion → PostgreSQL → retrieval pipeline → API integration |\n| **[NexoraAgri](https://github.com/deekshitaa1/NexoraAgri)** | Application Engineering | Data validation → application logic → service integration → decision support |"
    ),
    (
        "01  START WITH THE BUSINESS QUESTION\n02  VALIDATE DATA BEFORE MODELING\n03  KEEP ANALYSIS REPRODUCIBLE\n04  USE THE SIMPLEST EFFECTIVE MODEL\n05  CONNECT METRICS TO BUSINESS VALUE\n06  BUILD SYSTEMS THAT CAN BE EXPLAINED\n07  DEPLOYMENT IS PART OF ENGINEERING\n08  SHIP · MEASURE · ITERATE",
        "01  UNDERSTAND THE REQUIREMENTS\n02  CHOOSE THE RIGHT DATA STRUCTURES\n03  WRITE CLEAN, READABLE CODE\n04  DESIGN FOR FAILURE AND EDGE CASES\n05  TEST EARLY AND DEBUG SYSTEMATICALLY\n06  REVIEW FOR CORRECTNESS AND MAINTAINABILITY\n07  AUTOMATE BUILDS AND DEPLOYMENTS\n08  SHIP · MONITOR · ITERATE"
    ),
    (
        "### SOFTWARE DEVELOPMENT · SYSTEM DESIGN · CLOUD",
        "### SOFTWARE DEVELOPMENT · DATA STRUCTURES & ALGORITHMS · SYSTEM DESIGN"
    ),
    (
        "`01010011 01001111 01000110 01010100 01010111 01000001 01010010 01000101 00100000 01000101 01001110 01000111 01001001 01001110 01000101 01000101 01010010 01001001 01001110 01000111`",
        "`01010011 01001111 01000110 01010100 01010111 01000001 01010010 01000101 00100000 01000100 01000101 01010110 01000101 01001100 01001111 01010000 01001101 01000101 01001110 01010100`"
    )
]

for old, new in replacements:
    if old not in text:
        print("WARNING: replacement pattern not found:", old[:90].replace("\n", " "))
    text = text.replace(old, new, 1)

# Fix an existing unclosed code fence in the deployment section and retain the following sections.
text = text.replace(
    "        ↓\n        ↓\n        ↓\n        ↓\n        ↓\n        ↓\n        ↓\n        ↓\n        ↓\n        ↓\nSCALABLE SOFTWARE\n---",
    "        ↓\nSCALABLE SOFTWARE\n```\n\n---",
    1
)
# If original indentation differs, repair the known boundary directly.
if "SCALABLE SOFTWARE\n---\n\n<div align=\"center\">\n\n## `~/` contribution activity" in text:
    text = text.replace(
        "SCALABLE SOFTWARE\n---\n\n<div align=\"center\">\n\n## `~/` contribution activity",
        "SCALABLE SOFTWARE\n```\n\n---\n\n<div align=\"center\">\n\n## `~/` contribution activity",
        1
    )

# Keep the profile photo and animated contribution snake intact; output the full updated README.
out = Path("/mnt/data/README_SDE.md")
out.write_text(text, encoding="utf-8")
print(f"Created {out}; {len(text.splitlines())} lines.")
