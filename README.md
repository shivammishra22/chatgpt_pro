import pymupdf4llm
import pathlib

def pdf_to_markdown(pdf_path: str, md_output_path: str, *, pages=None, write_images=False, image_path="images", image_format="png", dpi=150):
    """
    Convert a PDF to Markdown.
    
    Args:
        pdf_path: Path to the PDF file.
        md_output_path: Path to save the output Markdown.
        pages: Optional list of 0-based page numbers to include.
        write_images: Whether to extract images and reference them in Markdown.
        image_path: Directory to store extracted images.
        image_format: Format of extracted images (e.g., "png", "jpg").
        dpi: Resolution for image extraction.
    """
    # Convert PDF to Markdown string
    md_text = pymupdf4llm.to_markdown(
        doc=pdf_path,
        pages=pages,
        write_images=write_images,
        image_path=image_path,
        image_format=image_format,
        dpi=dpi
    )
    
    # Save to markdown file
    pathlib.Path(md_output_path).write_text(md_text, encoding="utf-8")
    print(f"✅ Markdown saved to {md_output_path}")

if __name__ == "__main__":
    pdf_to_markdown(
        pdf_path="input.pdf",
        md_output_path="output.md",
        pages=None,                 # process all pages
        write_images=True,          # extract images
        image_path="images",        # store in ./images/
        image_format="png",
        dpi=150
    )
