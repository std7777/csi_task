# Binary Exploitation & Flag Retrieval

1. find the file type of the provided file.
   ```
   file ccs26_challenge
   ccs26_challenge: Bourne-Again shell script executable (binary data)

2.On inspecting,  it was found to have a Bash wrapper and embedded binary content.
<img width="1712" height="1032" alt="image" src="https://github.com/user-attachments/assets/ad8cbfc7-f0c5-4bee-bb6f-cfbcf7b109a2" />

<img width="1712" height="1032" alt="image" src="https://github.com/user-attachments/assets/aa1bb485-bb7b-400a-bf70-6aaa611ba25f" />

3. as the question suggests the first flag can be found through binary analysis so we proceed to extract the binary content. we look for the ELF byt
