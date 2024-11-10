# CleanBagel: Automated Data Preparation Pipeline

This repository contains the implementation of CleanBagel, an automated data preparation pipeline specifically optimized for Llama 3.2 fine-tuning. The implementation covers the first two days of development, focusing on core infrastructure, cleaning pipeline, annotation system, and quality control.

## Project Structure
```
cleanbagel/
├── src/
│   ├── __init__.py
│   ├── annotator.py
│   ├── cleaner.py
│   ├── pipeline.py
│   ├── quality_control/
│   │   ├── __init__.py
│   │   └── metrics.py
│   ├── quality_controlling.py
│   └── s3_connector.py
├── tests/
│   ├── __init__.py
│   ├── test_cleaner.py
│   ├── test_annotation_system.py
│   └── test_quality_control.py
├── config/
│   └── quality_config.json
├── requirements.txt
└── run.py
```

## Installation

1. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Install spaCy language model:
```bash
python -m spacy download en_core_web_sm
```

## Configuration

1. Set up AWS credentials for S3 access:
```bash
# ~/.aws/credentials
[default]
aws_access_key_id = your_access_key
aws_secret_access_key = your_secret_key
```

2. Create quality control configuration (config/quality_config.json):
```json
{
    "min_completeness": 0.8,
    "min_consistency": 0.7,
    "min_validity": 0.8,
    "min_uniqueness": 0.9,
    "max_data_age_days": 30,
    "min_accuracy": 0.8,
    "text_length_threshold": 10,
    "min_overall_score": 0.75,
    "output_dir": "quality_reports"
}
```

## Day 1 Implementation

### Core Infrastructure & Cleaning Pipeline

1. Run the basic cleaning pipeline:
```bash
python run.py
```

2. Run tests for the cleaning components:
```bash
python -m unittest tests/test_cleaner.py
```

### Monitoring the Pipeline

Check the logs in `pipeline.log` for detailed execution information.

## Day 2 Implementation

### Annotation System

1. Test the annotation system:
```bash
python -m unittest tests/test_annotation_system.py
```

2. Process a single file with annotations:
```bash
python -m src.pipeline --file your_file.csv --annotate
```

### Quality Control

1. Run quality control on a dataset:
```bash
python -m src.quality_controlling your_dataset.csv
```

2. Run with custom configuration:
```bash
python -m src.quality_controlling your_dataset.csv --config config/quality_config.json
```

3. Run quality control tests:
```bash
python -m unittest tests/test_quality_control.py
```

## Pipeline Components

### Day 1 Components:

1. **AdvancedCleaner**
   - Text cleaning and normalization
   - Boilerplate removal
   - Format standardization
   - Quality validation

2. **Pipeline Infrastructure**
   - S3 connectivity
   - Batch processing
   - Error handling
   - Logging

### Day 2 Components:

1. **AnnotationSystem**
   - Named Entity Recognition
   - Sentiment Analysis
   - Topic Detection
   - Keyword Extraction
   - Language Detection

2. **QualityControl**
   - Data completeness validation
   - Consistency checking
   - Validity assessment
   - Uniqueness verification
   - Custom validation rules

## Output Structure

### Quality Reports
```
quality_reports/
├── quality_report_dataset1_20241110_123456.json
├── quality_report_dataset1_20241110_123456.txt
├── quality_report_dataset2_20241110_123457.json
└── quality_report_dataset2_20241110_123457.txt
```

### Processed Data
```
processed_data/
├── processed_dataset1.csv
├── processed_dataset1_metrics.json
├── processed_dataset2.csv
└── processed_dataset2_metrics.json
```

## Testing

Run all tests:
```bash
python -m unittest discover tests
```

Run specific test suites:
```bash
python -m unittest tests/test_cleaner.py
python -m unittest tests/test_annotation_system.py
python -m unittest tests/test_quality_control.py
```

## Monitoring and Logging

- Pipeline logs: `pipeline.log`
- Quality control logs: `quality_control.log`
- Rich console output for quality metrics
- Detailed JSON reports for each processed dataset

## Error Handling

The pipeline includes comprehensive error handling:
- S3 connection issues
- File processing errors
- Data validation failures
- Quality control violations

Check the log files for detailed error information.

## Development Roadmap

### Day 1 ✅
- [x] Environment setup
- [x] Core infrastructure
- [x] Basic cleaning pipeline
- [x] Initial testing

### Day 2 ✅
- [x] Annotation system
- [x] Quality control implementation
- [x] Integration testing
- [x] Documentation

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## Support

For any issues or questions, please check:
1. The logs in `pipeline.log` and `quality_control.log`
2. The generated quality reports
3. The test results

If the issue persists, please create a GitHub issue with:
- Detailed description of the problem
- Relevant log excerpts
- Steps to reproduce