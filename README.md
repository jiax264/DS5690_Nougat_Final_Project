# Scanned PDF to Word Document Converter using Nougat (Neural Optical Understanding for Academic Documents)

## Motivation
My project, titled “Scanned PDF to Word Document Converter,” focuses on a service we provide at Vanderbilt's Disability Service Office. We transform scanned textbook pages in PDF format to Word documents. For blind students, this conversion to word format is about accessibility because screen readers oftentimes cannot effectively process the PDF format. And even if you’re not blind, a lot of times just having text that you can copy and paste is very helpful for taking notes which you can’t do for PDFs that are photocopies. 

Our current approach involves using Optical Character Recognition (OCR) software, which extracts all text, dumps it into a Word doc, and then we have to go in and fix any inaccuracies produced by the OCR. 

Now, I'd like to present an example of a scanned textbook page. Considering how OCR technology operates—identifying text regions and matching them to known character patterns—I’m interested in your thoughts on potential challenges. Based on this page below, what do you think might cause issues either in OCR correctly identifying text or in our workflow? 

![image](https://github.com/jiax264/DS5690_Nougat_Final_Project/assets/64748973/52064d46-fa21-4ac2-aa10-dc52a44b6549)
![image](https://github.com/jiax264/DS5690_Nougat_Final_Project/assets/64748973/b740e7e8-8253-4b93-920d-8f6197e0baa5)
### OCR Recognition Issues
- Page slightly rotated.
- Handwritten highlights/underlines.
- Words on the top right are larger and smeared.
- Part of the text on the bottom left is cut off.

### Workflow Issues Requiring Manual Editing
- OCR inadvertently captures page numbers and chapter headings, necessitating manual removal.
- New section headings require additional manual formatting.

## Comparison between Kurzweil OCR, ChatGPT-4, & Nougat 
Having pinpointed potential issues with OCR on poor quality scanned documents, let's now examine their actual impact on performance in a more concrete manner.
[Comparison](https://docs.google.com/document/d/1ykknJjCQ522MkBZKdvObo1KkGHpOF0kbGUwhGVEt4uw/edit?usp=sharing https://github.com/clovaai/donut/tree/master)

### Why my Approach is Superior 
My approach in this project offers advantages over using ChatGPT-4. With ChatGPT-4, you're limited to processing only a few images at a time; it can't handle an entire PDF. This means capturing screenshots page by page, waiting for each to process before moving on. Using the GPT-4 API, on the other hand, incurs a cost per use. In contrast, my method with Nougat allows for the entire PDF to be uploaded at once. It processes the document and automatically downloads a correctly formatted Word document to your computer, all free of charge.

## More about Nougat 
Before demonstrating the code, let me briefly discuss Nougat, the model used in this project. Nougat is designed to convert PDF text into markup language, building on the Donut architecture I covered in my paper presentation. This architecture, an encoder-decoder framework, enables end-to-end training without relying on OCR. As shown below, Nougat utilizes the Swin transformer from Donut, which divides an image into patches and applies self attention across the different patches. Additionally, it employs a BART-based decoder, but this one is one that is specifically tailored for scientific texts. Nougat was built to process texts from scientific research papers, often filled with mathematical equations and citations, hence its output in markdown format.

![image](https://github.com/jiax264/DS5690_Nougat_Final_Project/assets/64748973/25dd4bf3-bf51-43a2-ab43-44686f734907)
![image](https://github.com/jiax264/DS5690_Nougat_Final_Project/assets/64748973/5d8f7791-bb6d-4e9e-9986-52923efb8ae4)

A key aspect that sets the Nougat model apart is the diverse data augmentation techniques used during its training. As illustrated in this figure below, the model was exposed to various data manipulations like blurring, bolding text, rotating, and altering brightness. This diversity in training contributes significantly to the model's robustness. Given the varying quality of scanned documents, as exemplified in my earlier demonstration, incorporating such distortion and dirtiness into training enhances the model's ability to handle real-world scenarios effectively.
![image](https://github.com/jiax264/DS5690_Nougat_Final_Project/assets/64748973/302be7dc-daa7-4c63-b778-e6709ec5f59f)

## Code Demo
[Colab Notebook](https://colab.research.google.com/drive/1GkSS4vp6iQ8mG76XH5axgDsz7zRzehC8?usp=sharing)

## Project Impact & Next Steps
Once I introduce this notebook to my manager at Student Access, I hope it’s something that he uses because it will expedite our PDF to Word conversion process. 

Next steps involve fine-tuning the optimal hyperparameters for a variety of document types. Currently, the adjustments are based on a specific set of around 30 divinity PDF readings I've worked with. Additionally, integrating a captioning transformer model would be beneficial, particularly for textbooks with figures, enabling automatic captioning in the initial pass. Ultimately, deploying this solution on a Hugging Face space would be a valuable advancement.

## Resource Links
- [Nougat Hugging Face Documentation](https://huggingface.co/docs/transformers/en/model_doc/nougat)
- [Nougat Small Model](https://huggingface.co/facebook/nougat-small)
- [Nougat Base Model](https://huggingface.co/facebook/nougat-base)
- [Nougat Code Repository](https://github.com/facebookresearch/nougat)
- [Nougat Academic Paper](https://arxiv.org/pdf/2308.13418.pdf)
- [Donut Code Repository](https://github.com/clovaai/donut/tree/master)
- [Donut Academic Paper](https://arxiv.org/pdf/2111.15664.pdf)
