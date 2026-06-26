# PDF Batch DRM Protection Script (PHP)

`drm-protector-batch.php` is a PHP CLI script for batch processing PDF files.

The script recursively scans an input directory, uploads each PDF file to a DRM protection service, applies content protection, and downloads the protected files into an output directory while preserving the original directory structure.

This tool is intended for command-line use and is suitable for batch processing large collections of PDF documents.

---

## Features

- Batch process PDF files
- Recursive directory scanning
- Preserve original folder structure
- Automatically skip files already processed
- Safe to run multiple times
- Resume processing after temporary upload failures

---

## Requirements

- PHP 7.4 or later
- PHP CLI
- PHP cURL extension
- Internet connection

Verify that cURL is enabled:

```bash
php -m | grep curl
```

---

## Usage

```bash
php drm-protector-batch.php <input_directory> <output_directory>
```

Example:

```bash
php drm-protector-batch.php /data/original_pdfs /data/protected_pdfs
```

The script will:

1. Scan the input directory recursively.
2. Upload each PDF.
3. Apply DRM protection.
4. Download the protected `.vpdf` file.
5. Preserve the original directory structure.

---

## Parameters

### `<input_directory>`

Directory containing the source PDF files.

- All `.pdf` files are processed recursively.
- Non-PDF files are ignored.

### `<output_directory>`

Directory where protected files will be saved.

- Missing directories are created automatically.
- Original folder structure is preserved.

---

## Configuration

The script associates uploaded files with the email address configured in the source code:

```php
'Email' => 'your-email@example.com'
```

Ensure that this email address matches the intended DRM account before running the script.

---

## Recommended Workflow

Before processing a large number of files:

1. Test with one or two PDFs.
2. Verify the generated output.
3. Confirm that the correct account is being used.
4. Process the remaining files.

---

## Upload Limits

The remote DRM service may enforce temporary upload rate limits.

As a result:

- Some files may not be processed during a single run.
- Temporary upload failures are expected and can be retried.

---

## Safe to Re-run

The script is idempotent.

Before uploading a PDF, it checks whether the corresponding protected file already exists.

If the output file is present, that PDF is skipped automatically.

Running the script multiple times will:

- Skip files already processed.
- Retry files skipped previously.
- Continue until all PDFs have been protected.

Example:

```bash
php drm-protector-batch.php <input_directory> <output_directory>
```

---

## Large Batch Processing

For large collections of PDFs:

1. Run the script.
2. Wait until it finishes.
3. Run it again if necessary.
4. Repeat until no additional files are processed.

This approach works well when temporary upload limits are encountered.

---

## Documentation

Additional documentation:

- [PDF Content Security](https://verydrm.com/pdf-content-protection.php)
- [Video Content Security](https://verydrm.com/video-content-protection.php)
- [Audio Content Security](https://verydrm.com/audio-content-protection.php)

A DRM service account is required to upload, protect, and download protected files.

---

## License

Please refer to the project license for usage terms.
