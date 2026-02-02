# Court Decision Extraction Program - Design Document

## Overview

A Python program that extracts structured information from court decision documents using AI and outputs the data to a professional Excel spreadsheet.

## Architecture

### Components

1. **Document Parser** - Reads court decision documents (PDF, TXT, DOCX)
2. **AI Extractor** - Uses LLM to extract structured information based on predefined schema
3. **Excel Generator** - Creates professional Excel output with extracted data

### Technology Stack

- **Python 3.11**
- **OpenAI API** (gpt-4.1-mini) - For intelligent text extraction
- **openpyxl** - For Excel generation
- **PyPDF2/pdfplumber** - For PDF parsing
- **python-docx** - For DOCX parsing

## Extraction Schema

### Field Definitions

| Field Name | Query Type | Classification Options |
|------------|------------|------------------------|
| Case Name | Free response | - |
| Court | Free response | - |
| Judge(s) | Free response | - |
| Court Type | Classify | State OR Federal |
| Parties | Free response | - |
| Counsel | Free response | - |
| Subject Matter | Classify | Intellectual Property, Contract, Tort, Civil Rights, Constitutional, Antitrust, Criminal, State Regulatory, Federal Regulatory, Other |
| Procedural History | Free response | - |
| Procedural Posture | Free response | - |
| Claim(s) | Free response | - |
| Holding(s) | Free response | - |
| Statutes Cited | Free response | - |
| Cases Cited | Free response | - |
| Order | Free response | - |
| Concurrence | Free response | - |
| Dissent | Free response | - |

## Program Flow

1. **Input**: User provides court decision document(s)
2. **Parse**: Extract text from document
3. **Extract**: Send text to LLM with structured prompt
4. **Validate**: Check extracted data for completeness
5. **Output**: Generate Excel file with results

## Excel Output Design

### Sheet Structure

- **Single sheet** with all extracted data
- **Column headers** for each field
- **One row per court decision**
- **Professional formatting** following excel-generator skill guidelines

### Features

- Freeze panes for headers
- Auto-filter enabled
- Proper column widths
- Text wrapping for long content
- Professional theme (Elegant Black)
- Data validation indicators

## Implementation Strategy

### Phase 1: Core Extraction
- Implement document parsing
- Create LLM extraction logic
- Handle single document

### Phase 2: Excel Output
- Generate professional Excel file
- Apply formatting and styling
- Add metadata

### Phase 3: Batch Processing
- Support multiple documents
- Progress tracking
- Error handling

## Error Handling

- Missing fields: Mark as "Not found" or "N/A"
- Parsing errors: Log and continue with available data
- API errors: Retry with exponential backoff
