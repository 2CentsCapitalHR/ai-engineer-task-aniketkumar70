# 🏛️ ADGM Corporate Agent

AI-Powered Legal Document Intelligence & Compliance Checker for Abu Dhabi Global Market (ADGM)

## 📋 Overview

The ADGM Corporate Agent is an intelligent document analysis system designed to help legal professionals, corporations, and consultants ensure compliance with Abu Dhabi Global Market regulations. The system uses advanced AI, including Retrieval-Augmented Generation (RAG) technology, to analyze legal documents and provide detailed compliance feedback.

### 🌟 Key Features

- **Automated Document Analysis**: Reviews DOCX and PDF files for ADGM compliance
- **Process Detection**: Automatically identifies legal processes (Company Incorporation, Employment, Branch Registration, Data Protection)
- **Compliance Checking**: Validates documents against specific ADGM regulations
- **Document Annotation**: Adds review comments directly to DOCX files with severity-coded issues
- **Completeness Verification**: Checks if all required documents are present for a process
- **RAG-Enhanced Analysis**: Uses ADGM reference documents for accurate, context-aware guidance
- **Comprehensive Reporting**: Generates detailed JSON reports with compliance scores and recommendations

### 📚 Supported Document Types

#### Company Formation
- Articles of Association
- Memorandum of Association
- Board Resolutions
- Incorporation Application Forms
- Business Plans
- UBO Declarations

#### Employment & HR
- Employment Contracts (ER 2019 & ER 2024 compliant)
- HR Policies
- Disciplinary Procedures
- Grievance Procedures

#### Data Protection
- Appropriate Policy Documents (APD)
- Privacy Notices
- Record of Processing Activities (RoPA)
- Data Protection Impact Assessments

#### Branch Registration
- Parent Company Documents
- Audited Financial Statements
- Registration Applications
- Authorized Signatories Documentation

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- At least 4GB RAM (8GB recommended for optimal performance)
- Internet connection for downloading ML models

### Installation

1. **Clone or download the project**
   ```bash
   git clone <repository-url>
   cd adgm-corporate-agent
   ```
   Or simply download the `2cent_Assignment.ipynb` file.

2. **Set up Python environment** (recommended)
   ```bash
   python -m venv adgm_env
   source adgm_env/bin/activate  # On Windows: adgm_env\Scripts\activate
   ```

3. **Install required packages**
   
   The system will automatically install all required packages when you run it for the first time. Required packages include:
   - gradio>=4.46.0
   - python-docx
   - PyPDF2
   - sentence-transformers
   - faiss-cpu
   - torch
   - transformers
   - pandas
   - numpy
   - unidecode
   - datasets

4. **Prepare reference documents** (Optional but recommended)
   
   Place your ADGM reference documents in the specified paths:
   ```
   /content/ADGM CHECKLIST 2.pdf
   /content/ADGM checklist.pdf
   /content/ADGM Standard Employment Contract - ER 2019 - Short Version (May 2024).docx
   /content/ADGM Standard Employment Contract Template - ER 2024 (Feb 2025).docx
   /content/Data Sources.docx
   /content/OFFICE OF DATA PROTECTION.pdf
   /content/adgm-ra-resolution-multiple-incorporate-shareholders-LTD-incorporation-v2.docx
   ```
   
   If you don't have these files, the system will still work but with reduced reference capabilities.

### 🖥️ Running the Application

#### Option 1: Jupyter Notebook (Recommended for Google Colab)

1. **Upload the notebook to Google Colab**
   - Go to [Google Colab](https://colab.research.google.com)
   - Upload the `2cent_Assignment.ipynb` file
   - Run all cells

2. **Local Jupyter**
   ```bash
   jupyter notebook 2cent_Assignment.ipynb
   ```
   Then run all cells in the notebook.

#### Option 2: Direct Python Execution

1. **Extract the Python code from the notebook**
   
   Save the main code as `adgm_agent.py` and run:
   ```bash
   python adgm_agent.py
   ```

2. **Access the web interface**
   
   The system will provide:
   - Local URL: `http://localhost:7860`
   - Public URL: A gradio.live link for sharing

### 📁 File Structure

```
adgm-corporate-agent/
├── 2cent_Assignment.ipynb          # Main notebook file
├── README.md                       # This file
├── reference_documents/            # ADGM reference documents (optional)
│   ├── ADGM_CHECKLIST_2.pdf
│   ├── employment_contracts/
│   └── ...
└── temp_analysis/                  # Temporary files (auto-created)
```

## 🔧 Usage Guide

### Step 1: Upload Documents

1. Click the "📁 Upload Legal Documents" area
2. Select one or more DOCX or PDF files
3. Supported file types: `.docx`, `.pdf`

### Step 2: Analyze Documents

1. Click "🔍 Analyze Documents" button
2. Wait for the analysis to complete (typically 30-60 seconds)
3. Review the results in two sections:
   - **Analysis Summary**: Quick overview with compliance scores
   - **Detailed JSON Report**: Complete analysis results

### Step 3: Review Results

The system provides:

- **Process Detection**: Automatically identified legal process
- **Document Completeness**: Percentage of required documents uploaded
- **Compliance Score**: Overall compliance rating (0-100)
- **Issues Breakdown**: Categorized by severity (High/Medium/Low)
- **Missing Documents**: List of required documents not yet uploaded
- **Annotated Files**: DOCX files with review comments added

### Step 4: Download Annotated Files

- DOCX files will be annotated with review comments
- Comments are color-coded by severity:
  - **Red**: High severity issues
  - **Orange**: Medium severity issues
  - **Blue**: Low severity issues

## ⚙️ Configuration

### Customizing Reference Documents

Edit the `REFERENCE_FILES` dictionary in the code to point to your reference documents:

```python
REFERENCE_FILES = {
    'checklist_1': '/path/to/your/ADGM_CHECKLIST_2.pdf',
    'employment_2024': '/path/to/your/employment_contract.docx',
    # Add more as needed
}
```

### Adjusting Analysis Parameters

Key parameters can be modified:

```python
# Compliance scoring weights
FIELD_SCORE_WEIGHT = 70    # Weight for required fields
JURISDICTION_SCORE = 20    # Weight for jurisdiction compliance
GOVERNING_LAW_SCORE = 10   # Weight for governing law

# RAG search parameters
RAG_TOP_K = 5             # Number of relevant chunks to retrieve
RELEVANCE_THRESHOLD = 0.3  # Minimum relevance score
```

### Adding New Document Types

Extend the `DOCUMENT_TYPES` dictionary:

```python
DOCUMENT_TYPES["new_document_type"] = {
    "keywords": ["keyword1", "keyword2", "keyword3"],
    "weight": 1.0
}
```

## 🧪 Testing

### Running Built-in Tests

Uncomment and run the test function:

```python
test_system_with_sample_documents()
```

### Manual Testing

1. **Test with sample employment contract**:
   - Upload an employment contract DOCX
   - Verify it's detected as "employment_contract"
   - Check for missing required fields

2. **Test with corporate documents**:
   - Upload Articles of Association
   - Verify process detection as "Company Incorporation"
   - Review compliance issues

3. **Test completeness checking**:
   - Upload partial document set
   - Verify missing documents are correctly identified

## 📊 Understanding Results

### Compliance Scores

- **90-100**: Excellent compliance
- **75-89**: Good compliance
- **50-74**: Needs improvement
- **0-49**: Poor compliance - significant issues

### Issue Severity Levels

- **High**: Must be fixed before submission (affects core compliance)
- **Medium**: Should be addressed for better compliance
- **Low**: Minor issues or recommendations

### Process Types

1. **Company Incorporation**: Full company setup in ADGM
2. **Branch Registration**: Foreign company branch registration
3. **Employment/HR**: Employment documentation compliance
4. **Data Protection**: GDPR/data protection compliance

## 🚨 Troubleshooting

### Common Issues

1. **"No files uploaded" error**
   - Ensure files are properly selected before clicking analyze
   - Check file types are .docx or .pdf

2. **"RAG embeddings model failed to initialize"**
   - Check internet connection
   - Restart the application
   - Use keyword search fallback (automatic)

3. **"Error processing document"**
   - Ensure DOCX files are not corrupted
   - Try converting PDF to DOCX for better analysis
   - Check file permissions

4. **Low compliance scores**
   - Review detailed issues in the JSON report
   - Check annotated DOCX files for specific problems
   - Ensure correct document type is being analyzed

### Performance Issues

1. **Slow analysis**
   - Large files take longer to process
   - Multiple files increase processing time
   - Consider upgrading to GPU-enabled environment

2. **Memory issues**
   - Close other applications
   - Process fewer files at once
   - Use smaller reference document set

### Getting Help

1. **Check the detailed JSON report** for specific error messages
2. **Review the console output** in Jupyter notebook for technical errors
3. **Verify file integrity** by opening documents manually
4. **Test with minimal document set** to isolate issues

## 🔒 Security & Privacy

- Documents are processed locally and temporarily
- No documents are stored permanently
- No data is sent to external services (except for ML model downloads)
- Temporary files are automatically cleaned up
- All processing happens in your environment

## 📄 Legal Disclaimer

This automated review system is for guidance only. The analysis provided:

- Should not be considered as legal advice
- May not catch all compliance issues
- Requires professional legal review for final verification
- Is based on available ADGM regulations at the time of development
- Should be used as a preliminary assessment tool only

Always consult with qualified legal professionals for final compliance verification before submitting documents to ADGM authorities.

## 🤝 Contributing

This project is designed to be extensible. Areas for contribution:

1. **Additional Document Types**: Add support for new ADGM document types
2. **Enhanced Analysis**: Improve detection algorithms for specific compliance issues
3. **Reference Documents**: Add more ADGM reference materials to the knowledge base
4. **UI Improvements**: Enhance the Gradio interface
5. **Performance Optimization**: Improve processing speed and memory usage

## 📋 Requirements Summary

### System Requirements
- Python 3.8+
- 4GB+ RAM
- 2GB+ disk space
- Internet connection (initial setup)

### Python Dependencies
All dependencies are automatically installed:
- gradio>=4.46.0 (Web interface)
- python-docx (DOCX processing)
- PyPDF2 (PDF processing)
- sentence-transformers (AI embeddings)
- faiss-cpu (Vector search)
- torch (ML framework)
- transformers (NLP models)
- pandas, numpy (Data processing)
- unidecode (Text normalization)

### Optional Files
- ADGM reference documents (improves analysis accuracy)
- Custom configuration files
- Additional document templates

## 🚀 Getting Started Checklist

- [ ] Install Python 3.8+
- [ ] Download/clone the project
- [ ] Set up virtual environment (optional but recommended)
- [ ] Run the notebook or Python script
- [ ] Access web interface at provided URL
- [ ] Upload test documents
- [ ] Review analysis results
- [ ] Download annotated files

---
### LINK OF DEMO VIDEO
https://drive.google.com/drive/folders/1ZgJRnir2H59Ut5TZFI2laS2xQbLp4AHp?usp=sharing

**Version**: 1.0
**Last Updated**: 2024
**License**: Educational/Research Use

For technical support or questions about ADGM compliance, consult with qualified legal professionals.
