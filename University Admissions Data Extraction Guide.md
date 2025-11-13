# University Admissions Data Extraction Guide

## Overview
This guide provides standardized procedures for extracting university admission requirements from South African university prospectuses for your career guidance application.

---

## 1. PREPARATION PHASE

### Before You Start
- [ ] Gather all prospectuses (PDFs preferred)
- [ ] Create a master folder structure: `data/[university_name]/[year]/`
- [ ] Set up version control (Git recommended)
- [ ] Create a tracking spreadsheet for extraction progress
- [ ] Review the JSON schema and taxonomy documents

### Tools Needed
- JSON validator (e.g., jsonlint.com)
- Text editor with JSON support (VS Code recommended)
- Spreadsheet for tracking (Google Sheets/Excel)

---

## 2. EXTRACTION WORKFLOW

### Step-by-Step Process

#### **Step 1: University Information**
1. Extract basic university details from prospectus cover/introduction
2. Verify official university name and abbreviation
3. Confirm contact details from admissions section
4. Note prospectus year clearly

**Common Pitfalls:**
- Using informal names (e.g., "Cape Town" instead of "University of Cape Town")
- Missing abbreviations used in course codes

#### **Step 2: Course Identification**
1. Work faculty by faculty
2. Extract ALL courses, not just popular ones
3. Note official course codes exactly as shown
4. Identify qualification type (BSc, BCom, BA, etc.)

**Watch Out For:**
- Courses with similar names but different codes
- Joint degree programs (list as separate entries if separately administered)
- Discontinued courses (skip unless marked as final intake year)

#### **Step 3: Admission Requirements - NSC**

**Critical Fields:**
- **APS (Admission Point Score):** Look for minimum score
- **Subject requirements:** Note EXACT minimum levels (1-7 scale)
- **Language requirements:** Both Home Language and First Additional Language
- **Endorsement type:** Bachelor's degree vs Diploma endorsement

**Conversion Table for Reference:**
| Achievement Level | % Range | Points |
|------------------|---------|--------|
| 7 | 80-100 | 7 |
| 6 | 70-79 | 6 |
| 5 | 60-69 | 5 |
| 4 | 50-59 | 4 |
| 3 | 40-49 | 3 |
| 2 | 30-39 | 2 |
| 1 | 0-29 | 1 |

**Subject Name Standardization:**
Use these EXACT names:
- "Mathematics" (not Maths, Math, Pure Mathematics)
- "Mathematical Literacy" (not Maths Lit)
- "Physical Sciences" (not Physical Science, Physics)
- "Life Sciences" (not Life Science, Biology)
- "English Home Language" or "English First Additional Language"
- "Accounting"
- "Business Studies"
- "Economics"
- "Geography"
- "History"
- "Agricultural Sciences"
- "Information Technology"
- "Computer Applications Technology"

#### **Step 4: International Qualifications**

**Common International Qualifications to Look For:**
1. **A-Levels** (UK/Cambridge International)
2. **IB (International Baccalaureate)**
3. **IGCSE/O-Levels**
4. **US High School Diploma + SAT/ACT/AP**
5. **Other African systems** (Kenyan KCSE, Nigerian WAEC, etc.)

**For Each Qualification Extract:**
- Country/region
- Minimum overall requirements (e.g., "3 A-Levels", "IB with 32 points")
- Subject-specific requirements with grades
- English proficiency requirements
- Any exemptions from English tests

**English Proficiency Tests - Standard Formats:**
- IELTS: "7.0 overall" or "7.0 overall with 7.0 in Academic Writing"
- TOEFL iBT: Score out of 120 (e.g., "100")
- TOEFL PBT: Score out of 677 (e.g., "600")
- Cambridge CAE/CPE: Grade (e.g., "Grade B")
- PTE Academic: Score (e.g., "65")

#### **Step 5: Career Outcomes**

**Job Roles Extraction:**
1. Look in sections titled: "Career Opportunities", "Graduate Careers", "Where Can This Take You?"
2. Match roles to taxonomy codes (ICT-001, FIN-001, etc.)
3. Assign seniority level realistically (most graduates = "Entry Level")
4. List 5-8 key roles, prioritizing most common/relevant

**Industries:**
- Extract from prospectus career sections
- Add logical industries even if not explicitly mentioned
- Use broad categories (e.g., "Financial Services" not "Retail Banking")

**Professional Bodies:**
- Extract EXACT names (e.g., "ECSA" = Engineering Council of South Africa)
- Note accreditation status if mentioned
- Common SA professional bodies:
  - SAICA (Chartered Accountants)
  - ECSA (Engineers)
  - SACAP (Psychologists)
  - SAICA (Legal practitioners)
  - HPCSA (Healthcare practitioners)
  - SACNASP (Natural scientists)

---

## 3. STANDARDIZATION RULES

### Must-Follow Conventions

**1. Subject Names**
- Always use full names from standardized list
- Never abbreviate
- Consistent capitalization

**2. Grade Formats**
- NSC: Use level (1-7) AND percentage if given
- A-Levels: Letter grades (A*, A, B, C, etc.)
- IB: Numeric scores (7 = highest, 1 = lowest)

**3. Course Names**
- Use exact official name from prospectus
- Include full qualification in brackets if helpful (e.g., "Computer Science (BSc)")

**4. Currency**
- Always "ZAR" for South African Rand
- Include year for all financial figures

**5. Dates**
- ISO format: YYYY-MM-DD
- "30 September" → "2025-09-30"

**6. URLs**
- Include https://
- Verify links are active
- Use official university domains only

---

## 4. QUALITY ASSURANCE CHECKLIST

### Before Marking "Complete"

**University Level:**
- [ ] All required fields populated
- [ ] University name matches official name exactly
- [ ] Contact details verified
- [ ] Metadata complete (prospectus year, extraction date, etc.)

**Course Level (for EACH course):**
- [ ] Course code matches prospectus exactly
- [ ] Faculty and department correctly assigned
- [ ] APS score is reasonable (typically 20-48 range)
- [ ] All required subjects have minimum levels
- [ ] At least 3-5 job roles listed with taxonomy codes
- [ ] Professional registration bodies named correctly
- [ ] No "TBC", "TBD", or placeholder text remains

**Data Validation:**
- [ ] JSON is valid (use validator)
- [ ] No duplicate course codes within university
- [ ] All job role_category codes exist in taxonomy
- [ ] All enum values match schema (e.g., qualification_type)
- [ ] Date formats are consistent (YYYY-MM-DD)

---

## 5. COMMON ISSUES & SOLUTIONS

### Issue 1: Ambiguous Requirements
**Problem:** "Good performance in Mathematics required"
**Solution:** Look for footnotes, use minimum faculty requirements, or note: "Exact level not specified - check with university"

### Issue 2: Combined Requirements
**Problem:** "Mathematics OR Mathematical Literacy (level 6)"
**Solution:** List both as separate entries in required_subjects, note equivalency

### Issue 3: Missing International Requirements
**Problem:** Prospectus only lists NSC requirements
**Solution:** Check university website's international students section, add note: "International requirements not in prospectus - verify with admissions"

### Issue 4: Vague Career Information
**Problem:** "Graduates work in various sectors"
**Solution:** Research typical careers for the discipline, add note: "Careers inferred from qualification type", use seniority_level: "Varies"

### Issue 5: Discontinued Courses
**Problem:** Course in old prospectus not in new one
**Solution:** Skip unless explicitly marked as "final intake", note discontinuation in extraction notes

---

## 6. EXTRACTION TIPS & TRICKS

### Efficient Navigation
- Use Ctrl+F / Cmd+F to search for keywords: "admission", "requirements", "career", "APS"
- Prospectus typically organized: Introduction → Faculties → Courses → Admissions → Services
- Check table of contents first

### Time-Saving Strategies
- Extract all Computer Science courses, then all Engineering, etc. (batch similar courses)
- Copy-paste common requirements across similar courses (adjust as needed)
- Create templates for each faculty (they often share base requirements)

### When in Doubt
- **Don't guess** - mark field as null or add to notes
- Use "verification_status": "needs_review" liberally
- Better to flag uncertainty than provide wrong data

---

## 7. FILE MANAGEMENT

### Naming Conventions
```
[UNIVERSITY_ABBREVIATION]_[YEAR]_data.json

Examples:
UCT_2025_data.json
Wits_2025_data.json
UP_2025_data.json
```

### Folder Structure
```
project_root/
├── data/
│   ├── UCT/
│   │   ├── 2025/
│   │   │   ├── UCT_2025_data.json
│   │   │   ├── prospectus.pdf
│   │   │   └── extraction_notes.md
│   ├── Wits/
│   │   └── 2025/
│   ├── ...
├── schema/
│   ├── university_schema.json
│   └── job_taxonomy.json
├── templates/
│   └── sample_extraction.json
└── validation/
    └── validate.py
```

### Version Control
- Commit after each complete university extraction
- Commit message format: `Add: [University] [Year] data extraction`
- Tag major milestones: `v1.0-10-universities-complete`

---

## 8. VALIDATION & REVIEW

### Self-Review Checklist
1. **Completeness:** All courses from prospectus included?
2. **Accuracy:** Spot-check 3 random courses against source
3. **Consistency:** Same subject names used throughout?
4. **Schema Compliance:** JSON validates against schema?
5. **Taxonomy Adherence:** All job codes exist in taxonomy?

### Peer Review (Recommended)
- Have someone else verify 10% of entries
- Focus on: APS scores, subject requirements, job roles
- Document any systematic errors found

### Automated Checks
Consider creating scripts to check:
- Duplicate course codes
- Invalid taxonomy codes
- APS scores outside reasonable range (15-50)
- Missing required fields
- Invalid date formats
- Broken URLs

---

## 9. DEALING WITH EDGE CASES

### Case 1: Course with Multiple Entry Points
**Example:** "BCom Accounting - Regular (APS 40) or Extended (APS 35)"
**Solution:** Create TWO separate course entries with different course codes

### Case 2: Joint/Concurrent Degrees
**Example:** "BSc/LLB - 5-year combined degree"
**Solution:** Single entry, note both qualifications in qualification_name field

### Case 3: Courses at Multiple Campuses
**Example:** "BEng available at Johannesburg and Pretoria campuses"
**Solution:** Single entry if requirements identical, add campus info in notes

### Case 4: Foundation/Extended Programs
**Example:** "Extended BSc - 4 years for students needing additional support"
**Solution:** Separate course entry, mark duration as 4 years, note "Foundation year included"

### Case 5: Postgraduate Diplomas vs Honours
**Example:** Some universities offer PGDip, others offer Honours for similar fields
**Solution:** Extract as shown, use correct qualification_type from schema enum

---

## 10. READY TO START

### Your First Extraction Session
1. **Start small:** Choose ONE faculty from ONE university
2. **Extract 3-5 courses completely**
3. **Validate JSON**
4. **Review against this guide**
5. **Refine your process**
6. **Scale up gradually**

### Time Estimates
- University header info: 10-15 minutes
- Per course (basic): 15-20 minutes
- Per course (comprehensive with careers): 25-35 minutes
- Full university (30 courses): 12-18 hours
- **50 universities target: ~600-900 hours of extraction work**

### Suggested Milestone Plan
- **Week 1:** Extract 2 universities (practice + refinement)
- **Weeks 2-10:** Extract 5-6 universities per week
- **Weeks 11-12:** Quality assurance and validation
- **Week 13:** Final review and compilation

---

## 11. GETTING HELP

### When Stuck
1. Check similar courses in same faculty for patterns
2. Review university website for clarification
3. Mark field for review and continue
4. Note specific questions in extraction_metadata.notes

### Key Questions to Ask Yourself
- "Is this data directly from the prospectus or inferred?"
- "Would a student understand these requirements clearly?"
- "Are job roles realistic for a fresh graduate?"
- "Have I used standardized names from the taxonomy?"

---

## APPENDIX A: South African University List (Suggested 50)

### Traditional Universities (11)
1. University of Cape Town (UCT)
2. University of the Witwatersrand (Wits)
3. University of Pretoria (UP)
4. Stellenbosch University (SU)
5. University of KwaZulu-Natal (UKZN)
6. Rhodes University (RU)
7. University of the Free State (UFS)
8. University of Johannesburg (UJ)
9. North-West University (NWU)
10. University of Limpopo (UL)
11. Walter Sisulu University (WSU)

### Universities of Technology (6)
12. Cape Peninsula University of Technology (CPUT)
13. Durban University of Technology (DUT)
14. Tshwane University of Technology (TUT)
15. Vaal University of Technology (VUT)
16. Central University of Technology (CUT)
17. Mangosuthu University of Technology (MUT)

### Comprehensive Universities (4)
18. University of South Africa (UNISA)
19. Nelson Mandela University (NMU)
20. University of Zululand (UNIZULU)
21. University of Venda (UNIVEN)

### Focus on Major Universities (top 50 spots)
22-50. Repeat above list with different faculties, add private institutions (e.g., Varsity College, Regent, Milpark, etc.) based on your target audience

---

## APPENDIX B: Faculty Standardization

**Use these exact faculty names:**
- Faculty of Engineering and the Built Environment
- Faculty of Health Sciences
- Faculty of Humanities
- Faculty of Law
- Faculty of Science
- Faculty of Commerce / Business and Economic Sciences
- Faculty of Education
- Faculty of Agriculture / Veterinary Science
- Faculty of Arts / Social Sciences

---

## APPENDIX C: Quick Reference - Required vs Optional Fields

### REQUIRED (Must Have)
- University name, country, province
- Course code, name, faculty, qualification_type
- NSC minimum APS
- At least ONE subject requirement
- At least ONE job role

### HIGHLY RECOMMENDED
- International qualifications (if in prospectus)
- English proficiency requirements
- Professional registration information
- Career outcomes with 3-5 job roles

### OPTIONAL (Nice to Have)
- Employment statistics
- Average salaries
- Course content details
- Fees information
- Accommodation info

---

**Remember:** Quality over speed. A well-extracted dataset of 20 universities is more valuable than a rushed dataset of 50 with errors.

**Final Note:** This is a living document. As you encounter new situations, update this guide for future reference.
