# Court Decision Extractor - User Guide

## Table of Contents

1. [Overview](#overview)
2. [Installation](#installation)
3. [Basic Usage](#basic-usage)
4. [Advanced Usage](#advanced-usage)
5. [Understanding the Output](#understanding-the-output)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)
8. [API Costs](#api-costs)

---

## Overview

The Court Decision Extractor is an AI-powered tool that automatically extracts structured information from court decisions and organizes it into a professional Excel spreadsheet. It uses advanced natural language processing to identify and extract 16 different categories of legal information.

### Key Features

- **Automated Extraction**: No manual reading or data entry required
- **Batch Processing**: Process multiple documents simultaneously
- **Professional Output**: Excel files with proper formatting and organization
- **Flexible Input**: Supports PDF, Word, and text formats
- **Intelligent Parsing**: Handles complex legal documents with AI

---

## Installation

### Prerequisites

- Python 3.11 or higher
- OpenAI API key
- Internet connection

### Step-by-Step Installation

1. **Navigate to the program directory**:
   ```bash
   cd court_extractor
   ```

2. **Install required packages**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure your API key**:
   
   **Option A - Environment Variable (Recommended)**:
   ```bash
   export OPENAI_API_KEY="sk-your-api-key-here"
   ```
   
   **Option B - Add to shell profile** (persistent):
   ```bash
   echo 'export OPENAI_API_KEY="sk-your-api-key-here"' >> ~/.bashrc
   source ~/.bashrc
   ```

4. **Verify installation**:
   ```bash
   python court_extractor.py --help
   ```

---

## Basic Usage

### Command Syntax

```bash
python court_extractor.py <file1> [file2] [file3] ...
```

### Example 1: Single Document

```bash
python court_extractor.py smith_v_jones.pdf
```

**Output**:
```
======================================================================
Court Decision Extractor
======================================================================
Found 1 file(s) to process

[1/1] Processing: smith_v_jones.pdf
Extracting information from smith_v_jones.pdf...
✓ Successfully extracted information

Generating Excel file: court_decisions_extracted_20260202_143022.xlsx
✓ Excel file created successfully
======================================================================
```

### Example 2: Multiple Documents

```bash
python court_extractor.py case1.pdf case2.pdf case3.docx
```

### Example 3: Using Wildcards

Process all PDFs in a directory:
```bash
python court_extractor.py cases/*.pdf
```

Process all supported formats:
```bash
python court_extractor.py cases/*
```

---

## Advanced Usage

### Organizing Your Files

**Recommended directory structure**:
```
project/
├── court_extractor.py
├── input_cases/
│   ├── case1.pdf
│   ├── case2.pdf
│   └── case3.docx
└── output/
    └── (generated Excel files)
```

**Run from project directory**:
```bash
python court_extractor.py input_cases/*.pdf
mv court_decisions_extracted_*.xlsx output/
```

### Processing Large Batches

For large numbers of documents, consider processing in batches:

```bash
# Process 10 files at a time
python court_extractor.py cases/batch1/*.pdf
python court_extractor.py cases/batch2/*.pdf
python court_extractor.py cases/batch3/*.pdf
```

### Handling Different File Types

The program automatically detects file types:

```bash
# Mix different formats
python court_extractor.py \
  opinions/decision1.pdf \
  opinions/decision2.docx \
  opinions/decision3.txt
```

---

## Understanding the Output

### Excel File Structure

The generated Excel file contains:

#### Metadata Section (Top)
- **Title**: "Court Decision Extraction Results"
- **Generation Date**: When the extraction was performed
- **Total Cases**: Number of documents processed

#### Data Table
Each row represents one court decision with the following columns:

| Column | Description | Example |
|--------|-------------|---------|
| **Source File** | Original filename | `smith_v_jones.pdf` |
| **Extraction Date** | Processing timestamp | `2026-02-02 14:30:22` |
| **Case Name** | Full case name | `Smith v. Jones` |
| **Court** | Issuing court | `United States District Court for the Southern District of New York` |
| **Judge(s)** | Presiding judge(s) | `Hon. Jane Smith` |
| **Court Type** | Classification | `Federal` or `State` |
| **Parties** | Involved parties | `Plaintiff: John Smith; Defendant: ACME Corp` |
| **Counsel** | Legal representatives | `For Plaintiff: Law Firm A; For Defendant: Law Firm B` |
| **Subject Matter** | Legal area | `Contract`, `Tort`, etc. |
| **Procedural History** | Case background | Summary of prior proceedings |
| **Procedural Posture** | Current status | `Appeal from summary judgment` |
| **Claim(s)** | Issues addressed | Summary of legal claims |
| **Holding(s)** | Court's decisions | Summary of holdings |
| **Statutes Cited** | Key statutes | `29 U.S.C. § 201 et seq.` |
| **Cases Cited** | Key precedents | `Anderson v. Liberty Lobby, Inc., 477 U.S. 242` |
| **Order** | Final order | `REVERSED and REMANDED` |
| **Concurrence** | Concurring opinion | Summary if present |
| **Dissent** | Dissenting opinion | Summary if present |

### Excel Features

✓ **Frozen Headers**: Scroll through data while keeping headers visible  
✓ **Auto-Filter**: Filter and sort by any column  
✓ **Text Wrapping**: Long content is wrapped for readability  
✓ **Alternating Colors**: Easier to read rows  
✓ **Professional Styling**: Clean, elegant appearance  

---

## Best Practices

### 1. Document Preparation

**Before processing**:
- Ensure PDFs are text-based (not scanned images)
- Check that files are not corrupted
- Remove any password protection
- Verify file extensions are correct

### 2. Batch Processing Strategy

**For best results**:
- Process similar document types together
- Start with a small test batch (3-5 documents)
- Review results before processing large batches
- Keep batches under 50 documents at a time

### 3. Quality Control

**After extraction**:
- Review the Excel file for accuracy
- Check for "N/A" entries that might need manual review
- Verify classification fields (Court Type, Subject Matter)
- Cross-reference critical information with source documents

### 4. File Management

**Organize your workflow**:
- Keep original documents in a separate folder
- Archive processed documents
- Save Excel outputs with descriptive names
- Maintain a processing log

### 5. Cost Management

**To minimize API costs**:
- Remove duplicate documents before processing
- Process only necessary documents
- Consider document length (longer = more expensive)
- Use batch processing to reduce overhead

---

## Troubleshooting

### Common Issues and Solutions

#### Issue: "No module named 'PyPDF2'"

**Cause**: Required packages not installed  
**Solution**:
```bash
pip install -r requirements.txt
```

#### Issue: "OpenAI API key not found"

**Cause**: API key not set in environment  
**Solution**:
```bash
export OPENAI_API_KEY="your-api-key-here"
```

#### Issue: "Error extracting text from PDF"

**Cause**: PDF may be scanned image or corrupted  
**Solutions**:
1. Try converting PDF to text first
2. Use OCR software to extract text
3. Check if PDF is password-protected
4. Verify PDF is not corrupted

#### Issue: "Rate limit exceeded"

**Cause**: Too many API requests in short time  
**Solution**:
- Wait 1-2 minutes between large batches
- Reduce batch size
- Check your OpenAI account rate limits

#### Issue: Inaccurate Extractions

**Cause**: Document format or content issues  
**Solutions**:
1. Verify document is a court decision
2. Check document formatting is standard
3. Review very long documents (may be truncated)
4. Manually verify critical information

#### Issue: "N/A" in Many Fields

**Cause**: Information not found in document  
**Solutions**:
1. Verify document contains the information
2. Check if document is complete
3. Review document formatting
4. Some fields may legitimately be absent (e.g., no dissent)

---

## API Costs

### Understanding Costs

The program uses OpenAI's API, which charges based on tokens processed:

- **Model**: gpt-4.1-mini
- **Typical cost per document**: $0.01 - $0.05
- **Factors affecting cost**:
  - Document length
  - Complexity of content
  - Number of documents

### Cost Estimation

| Document Type | Approx. Cost |
|---------------|--------------|
| Short opinion (5 pages) | $0.01 - $0.02 |
| Medium opinion (15 pages) | $0.02 - $0.03 |
| Long opinion (30+ pages) | $0.03 - $0.05 |

**Example**: Processing 100 medium-length opinions ≈ $2.00 - $3.00

### Cost Optimization Tips

1. **Remove duplicates** before processing
2. **Process only necessary documents**
3. **Use text format** when possible (smaller than PDF)
4. **Batch similar documents** together
5. **Monitor your OpenAI usage** dashboard

---

## Tips for Success

### Getting the Best Results

1. **Start Small**: Test with 2-3 documents first
2. **Review Output**: Check accuracy before processing large batches
3. **Standardize Input**: Use consistent document formats when possible
4. **Keep Backups**: Save original documents separately
5. **Document Your Process**: Note any issues or patterns you observe

### When to Use Manual Review

Consider manual verification for:
- High-stakes legal matters
- Documents with unusual formatting
- Cases with complex procedural histories
- Documents where many fields show "N/A"

### Enhancing Accuracy

- Provide complete, unredacted documents
- Ensure documents are official court opinions
- Use high-quality PDFs (not photocopies of photocopies)
- Process documents from the same jurisdiction together

---

## Support and Feedback

For technical issues or questions:
1. Check this user guide
2. Review the README.md
3. Consult the design.md for technical details

---

## Version Information

- **Version**: 1.0
- **Last Updated**: February 2, 2026
- **Python Version**: 3.11+
- **AI Model**: gpt-4.1-mini
