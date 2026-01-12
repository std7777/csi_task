# Binary Exploitation & Flag Retrieval

flag 1 = CTF{its_3am_might_just_git_push_force}
flag 2 = CTF{source_is_trust_me_bro}
flag 3 - CTF{touch_grass}

1. find the file type of the provided file.
   ```
   file ccs26_challenge
   ccs26_challenge: Bourne-Again shell script executable (binary data)
   ```

2. On inspecting,  it was found to have a Bash wrapper and embedded binary content.
<img width="1712" height="1032" alt="image" src="https://github.com/user-attachments/assets/ad8cbfc7-f0c5-4bee-bb6f-cfbcf7b109a2" />

3. As the question suggests the first flag can be found through binary analysis so we proceed to extract the binary content.
   a. we look for the magic bytes to confirm it is a ELF binary file. (linux executable)
      ```
      grep -a -n ELF ccs26_challenge
      ```
      -a: process binary as text
      -n: show line no.
   <img width="1712" height="1032" alt="image" src="https://github.com/user-attachments/assets/aa1bb485-bb7b-400a-bf70-6aaa611ba25f" />
      the binary data begins from line 27.

   b. to analyse the binary alone we extract it.
      ```
      tail -n +27 ccs26_challenge > data.bin
      ```
   tail : output last part of a files.
   -n +27 : output stats from 27 line. 
    > : output redirected to file data.bin .

   c. We check the file type of the resultant.
   <img width="663" height="745" alt="image" src="https://github.com/user-attachments/assets/1cbd6834-92fe-4d71-85db-bd634d68a8ab" />
   It is a tar archive.
4.  To find the flag we list its table of contents and spot a secret.txt file.
5.  We extracte the TAR archive file into a directory.
   ```
   mkdir extracted
   tar -xf data.bin -C extracted
   ```
6. We find the first flag in the secret.txt file.
   CTF{its_3am_might_just_git_push_force}
   <img width="1385" height="722" alt="image" src="https://github.com/user-attachments/assets/29188e52-456c-43ac-bfa7-74eba5cb7a6a" />

7. Trace_id are used to track requests but they aren't endoded in base64. On decoding the request we get flag 2.
   CTF{source_is_trust_me_bro}

  The endpoints found in secret.txt suggested a challenge is used by the application to retrieve flag 3.

8. On sending a GET request to the challenge endpoint, we receive a challenge question. 
  <img width="554" height="525" alt="Screenshot 2026-01-12 164716" src="https://github.com/user-attachments/assets/e479c386-1d2d-44c1-aa99-e61c8b123815" />

9. We decode the string and get ```hitler_liked_hello_kitty```
10. Due to TLS issues with command-line tools, Burp Suite was used to manually create and submit the HTTP request.
    <img width="1919" height="1071" alt="Screenshot 2026-01-12 020505" src="https://github.com/user-attachments/assets/fa470fa3-14b7-4919-a3d4-14b4c379a8b0" />

Thus, we get the last flag. 
"flag":"CTF{touch_grass}"

   
