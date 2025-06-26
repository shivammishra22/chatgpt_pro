from langchain_text_splitters import MarkdownTextSplitter

def split_markdown(md_file_path: str, chunk_size=500, chunk_overlap=50):
    # Load markdown content
    with open(md_file_path, "r", encoding="utf-8") as file:
        markdown_text = file.read()

    # Initialize MarkdownTextSplitter
    splitter = MarkdownTextSplitter(chunk_size=chunk_size, chunk_overlap=chunk_overlap)
    
    # Split markdown into chunks
    chunks = splitter.split_text(markdown_text)

    # Display chunk summary
    print(f"✅ Total Chunks: {len(chunks)}")
    for i, chunk in enumerate(chunks[:5]):
        print(f"\n--- Chunk {i+1} ---\n{chunk[:300]}...")  # Preview first 300 characters

    return chunks

# Example usage
if __name__ == "__main__":
    chunks = split_markdown("output.md")
