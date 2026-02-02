# Court Decision Extractor

A Python program that extracts structured background information and reasoning from court decisions using AI and outputs the data to a professional Excel spreadsheet.

## Features

- **Intelligent Extraction**: Uses OpenAI's GPT-4 to extract 16 categories of information from court decisions
- **Multiple Format Support**: Processes PDF, DOCX, and TXT files
- **Batch Processing**: Handle multiple court decisions in a single run
- **Professional Excel Output**: Generates formatted spreadsheets with proper styling, filters, and frozen headers
- **Error Handling**: Gracefully handles missing information and processing errors

## Extracted Information

The program extracts the following categories from each court decision:

### Free Response Fields
- Case Name
- Court
- Judge(s)
- Parties
- Counsel
- Procedural History
- Procedural Posture
- Claim(s)
- Holding(s)
- Statutes Cited
- Cases Cited
- Order
- Concurrence
- Dissent

### Classification Fields
- **Court Type**: State OR Federal
- **Subject Matter**: Intellectual Property, Contract, Tort, Civil Rights, Constitutional, Antitrust, Criminal, State Regulatory, Federal Regulatory, or Other

## Requirements

- Python 3.11 or higher
- OpenAI API key (set as `OPENAI_API_KEY` environment variable)
- Required packages (see `requirements.txt`)

## Installation

1. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Set up OpenAI API key**:
   ```bash
   export OPENAI_API_KEY="your-api-key-here"
   ```

## Usage

### Basic Usage

Process a single court decision:
```bash
python court_extractor.py decision.pdf
```

### Batch Processing

Process multiple court decisions:
```bash
python court_extractor.py decision1.pdf decision2.pdf decision3.docx
```

### Supported File Formats

- **PDF** (`.pdf`)
- **Word Documents** (`.docx`, `.doc`)
- **Text Files** (`.txt`)

## Output

The program generates an Excel file named `court_decisions_extracted_YYYYMMDD_HHMMSS.xlsx` with:

- **Professional formatting** with elegant black theme
- **Frozen header row** for easy scrolling
- **Auto-filter** enabled for all columns
- **Text wrapping** for long content
- **Alternating row colors** for readability
- **Metadata** including source file and extraction date

### Excel Structure

| Column | Description |
|--------|-------------|
| Source File | Original filename of the court decision |
| Extraction Date | Timestamp when the extraction was performed |
| Case Name | Name of the case |
| Court | Court that issued the opinion |
| Judge(s) | Judge(s) who issued the opinion |
| Court Type | State or Federal classification |
| Parties | Parties relevant to the opinion |
| Counsel | Representatives of the parties |
| Subject Matter | Legal area classification |
| Procedural History | Procedural history addressed in the opinion |
| Procedural Posture | Procedural posture of the case |
| Claim(s) | Issues addressed by the court |
| Holding(s) | Holdings in the opinion |
| Statutes Cited | Critical statutes cited |
| Cases Cited | Critical cases cited |
| Order | Final order in the case |
| Concurrence | Summary of concurrence analysis |
| Dissent | Summary of dissent analysis |

## Example

```bash
# Process three court decisions
python court_extractor.py \
  cases/smith_v_jones.pdf \
  cases/doe_v_roe.docx \
  cases/state_v_defendant.pdf

# Output:
# [1/3] Processing: cases/smith_v_jones.pdf
# Extracting information from smith_v_jones.pdf...
# ✓ Successfully extracted information
# 
# [2/3] Processing: cases/doe_v_roe.docx
# Extracting information from doe_v_roe.docx...
# ✓ Successfully extracted information
# 
# [3/3] Processing: cases/state_v_defendant.pdf
# Extracting information from state_v_defendant.pdf...
# ✓ Successfully extracted information
# 
# Generating Excel file: court_decisions_extracted_20260202_143022.xlsx
# ✓ Excel file created successfully
```

## Error Handling

- **Missing Information**: Fields that cannot be found are marked as "N/A"
- **Parsing Errors**: Documents that fail to parse are logged and skipped
- **API Errors**: Network or API issues are caught and reported
- **Invalid Files**: Non-existent or unsupported file types are identified before processing

## Technical Details

### AI Extraction

The program uses OpenAI's `gpt-4.1-mini` model with:
- **Low temperature** (0.1) for consistent, factual extraction
- **Structured prompts** with clear field definitions
- **JSON output** for reliable parsing
- **Text truncation** for very long documents (30,000 character limit)

### Excel Generation

Built using `openpyxl` with professional styling:
- **Theme**: Elegant Black (customizable)
- **Fonts**: Georgia for titles, Calibri for data
- **Layout**: Proper margins, spacing, and alignment
- **Features**: Frozen panes, auto-filter, text wrapping

## Limitations

- **Document Length**: Very long documents (>30,000 characters) are truncated
- **OCR**: Scanned PDFs without text layer may not extract properly
- **API Costs**: Each extraction uses OpenAI API tokens (typically $0.01-0.05 per document)
- **Accuracy**: AI extraction may occasionally miss or misinterpret information

## Troubleshooting

### "No module named 'PyPDF2'"
Install required packages: `pip install -r requirements.txt`

### "OpenAI API key not found"
Set your API key: `export OPENAI_API_KEY="your-key"`

### "Error extracting text from PDF"
Try converting the PDF to text format first, or ensure it's not a scanned image

### "Rate limit exceeded"
Wait a moment between large batch processing runs

## License

This program is provided as-is for legal research and analysis purposes.

## Support

For issues or questions, please refer to the design documentation in `design.md`.
