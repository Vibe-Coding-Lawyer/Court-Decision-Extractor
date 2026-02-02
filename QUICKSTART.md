# Quick Start Guide

## Getting Started in 3 Steps

### Step 1: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 2: Set Your OpenAI API Key

```bash
export OPENAI_API_KEY="your-api-key-here"
```

### Step 3: Run the Extractor

```bash
python court_extractor.py your_court_decision.pdf
```

That's it! The program will create an Excel file with all extracted information.

---

## Example Usage

### Single Document
```bash
python court_extractor.py case_decision.pdf
```

### Multiple Documents
```bash
python court_extractor.py case1.pdf case2.docx case3.txt
```

### Using Wildcards
```bash
python court_extractor.py cases/*.pdf
```

---

## What Gets Extracted?

The program automatically extracts:

✓ Case name and court information  
✓ Judges and parties involved  
✓ Legal subject matter classification  
✓ Procedural history and posture  
✓ Claims and holdings  
✓ Cited statutes and cases  
✓ Final order  
✓ Concurrence and dissent summaries  

---

## Output

You'll get a professional Excel file named:
```
court_decisions_extracted_YYYYMMDD_HHMMSS.xlsx
```

The Excel file includes:
- All extracted information in organized columns
- Frozen headers for easy scrolling
- Auto-filters for data exploration
- Professional formatting
- Source file tracking
- Extraction timestamps

---

## Tips

💡 **Batch Processing**: Process multiple files at once to save time  
💡 **File Formats**: Supports PDF, DOCX, and TXT files  
💡 **Long Documents**: Very long documents are automatically truncated to 30,000 characters  
💡 **Missing Data**: Fields that can't be found are marked as "N/A"  

---

## Troubleshooting

**Problem**: "No module named 'PyPDF2'"  
**Solution**: Run `pip install -r requirements.txt`

**Problem**: "OpenAI API key not found"  
**Solution**: Set your API key with `export OPENAI_API_KEY="your-key"`

**Problem**: PDF extraction fails  
**Solution**: Try converting the PDF to text first, or ensure it's not a scanned image

---

## Need More Help?

See the full README.md for detailed documentation.
