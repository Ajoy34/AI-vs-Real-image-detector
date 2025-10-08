# Converting LaTeX to Word Document for IDAA 2025 Submission

## Quick Method: Use Overleaf + Word Export

### Option 1: Overleaf to Word (EASIEST - RECOMMENDED)

1. **Upload to Overleaf:**
   - Go to https://www.overleaf.com
   - Sign up/Login (free)
   - Click "New Project" → "Upload Project"
   - Upload `IDAA_2025_Paper_Draft.tex`

2. **Compile to PDF first:**
   - Click "Recompile" in Overleaf
   - Verify PDF looks correct

3. **Export to Word:**
   - In Overleaf, click the "Download" menu
   - Select "Download as Word (.docx)"
   - OR: Download PDF, then use PDF to Word converter

---

## Option 2: Use Pandoc (Local Conversion)

### Install Pandoc:
**Windows:**
```powershell
# Using Chocolatey
choco install pandoc

# Or download installer from:
# https://pandoc.org/installing.html
```

### Convert LaTeX to Word:
```powershell
cd "C:\Users\ajoys\OneDrive\Desktop\Ai_image_detection"

# Basic conversion
pandoc IDAA_2025_Paper_Draft.tex -o IDAA_2025_Paper_Draft.docx

# With bibliography
pandoc IDAA_2025_Paper_Draft.tex --bibliography=references.bib -o IDAA_2025_Paper_Draft.docx

# With reference style
pandoc IDAA_2025_Paper_Draft.tex --citeproc -o IDAA_2025_Paper_Draft.docx
```

---

## Option 3: PDF to Word Conversion

If you already have the PDF compiled:

### Online Converters (Free):
1. **Adobe Online:** https://www.adobe.com/acrobat/online/pdf-to-word.html
2. **Smallpdf:** https://smallpdf.com/pdf-to-word
3. **iLovePDF:** https://www.ilovepdf.com/pdf_to_word
4. **PDF2Go:** https://www.pdf2go.com/pdf-to-word

### Steps:
1. Compile `IDAA_2025_Paper_Draft.tex` to PDF (using Overleaf)
2. Upload PDF to any converter above
3. Download resulting .docx file
4. Open in Microsoft Word
5. Fix any formatting issues

---

## Option 4: Manual Word Document Creation

I can create a pre-formatted Word document for you with all the content.
This will be ready to submit without any conversion needed.

**Advantages:**
- Guaranteed formatting
- No conversion errors
- Ready to submit immediately
- Can edit directly in Word

**Would you like me to create this?** 
(Note: I'll create a structured document with all sections, but you may need 
to adjust formatting in Word to match Springer guidelines exactly)

---

## Important Notes for Word Submission

### IDAA 2025 Requirements:
- ✅ Format: **PDF is required** (not .docx)
- ✅ Template: **Springer LNCS format**
- ✅ Even if you create in Word, you must submit as PDF

### Recommended Workflow:
1. Create Word document (for easier editing)
2. Format according to Springer guidelines
3. Export to PDF from Word
4. Submit PDF to conference

---

## Springer LNCS Word Template

### Download Official Template:
1. Go to: https://www.springer.com/gp/computer-science/lncs/conference-proceedings-guidelines
2. Look for "Word Template" or "Microsoft Word 2007 template"
3. Download `splncs04.dotx` or similar
4. Use this template to format your Word document

### Key Formatting Requirements:
- **Font:** Times New Roman, 10pt
- **Margins:** 
  - Top: 3.5cm
  - Bottom: 3cm
  - Left: 2.5cm
  - Right: 2.5cm
- **Line spacing:** Single
- **Title:** Bold, 14pt, centered
- **Abstract:** Italicized, with "Abstract" heading
- **Sections:** Bold, 12pt
- **References:** Numbered [1], [2], etc.

---

## What I Can Do For You RIGHT NOW:

### I can create:

1. **Formatted Word Document (.docx)** with all your content
   - All sections properly structured
   - Ready to edit in Microsoft Word
   - Includes all text from the LaTeX paper

2. **Simple Text Document (.txt)** with all content
   - Can copy-paste into Word template
   - All sections labeled

3. **Rich Text Format (.rtf)** 
   - Compatible with all word processors
   - Preserves basic formatting

**Which would you like me to create?**

---

## My Recommendation:

**Best approach for IDAA 2025:**

1. **Use Overleaf** (easiest):
   - Upload .tex file
   - Compile to PDF
   - Submit PDF directly
   - ✅ Perfect formatting guaranteed
   - ✅ No conversion issues

2. **If you prefer Word for editing:**
   - Let me create a Word document with all content
   - You format it in Word using Springer template
   - Export to PDF
   - Submit PDF

**Remember:** IDAA 2025 requires **PDF submission**, so even if you work in Word, 
you'll need to convert to PDF before submitting.

---

## Ready to Create Word Document?

Let me know if you want me to:
- [ ] Create a .docx file with all content (I'll do this now)
- [ ] Create a .txt file for copy-paste
- [ ] Just guide you to use Overleaf (easiest path)

**Shall I create the Word document now?** Type "yes" and I'll generate it immediately!
