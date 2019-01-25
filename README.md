# utl-sas-integration-of-ceasar-and-vigenere-ciphers-in-python-
SAS integration of ceasar and vigenere ciphers in python.
    SAS integration of ceasar and vigenere ciphers in python;                                                          
                                                                                                                       
      Two Ciphers                                                                                                      
                                                                                                                       
        1.  Caesar Cipher   https://www.geeksforgeeks.org/caesar-cipher/                                               
        2.  Vigenère Cipher https://www.geeksforgeeks.org/vigenere-cipher/                                             
                                                                                                                       
    Python seems to have issues with SASxport(v5), SPSS ..                                                             
    Only STATA output seems solid.                                                                                     
                                                                                                                       
    github                                                                                                             
    https://tinyurl.com/yab9u7vv                                                                                       
    https://github.com/rogerjdeangelis/utl-sas-integration-of-ceasar-and-vigenere-ciphers-in-python                    
                                                                                                                       
    Inspired by                                                                                                        
    https://tinyurl.com/ya2ljj6k                                                                                       
    https://communities.sas.com/t5/SAS-Programming/Data-masking-Implement-a-cipher/m-p/20644/highlight/true#M3237      
                                                                                                                       
    Other Python Ciphers                                                                                               
    ---------------------                                                                                              
                                                                                                                       
    Vigenère Cipher  ** below                                                                                          
    Caesar Cipher    ** below                                                                                          
                                                                                                                       
    XOR Cipher                                                                                                         
    Null Cipher                                                                                                        
    Baconian Cipher                                                                                                    
    ROT13 cipher                                                                                                       
    Hill Cipher                                                                                                        
    Columnar Transposition Cipher                                                                                      
    Implementing Atbash Cipher                                                                                         
    Implementation of Affine Cipher                                                                                    
    Polybius Square Cipher                                                                                             
    Latin alphabet cipher                                                                                              
    Rail Fence Cipher - Encryption and Decryption                                                                      
    Count all Prime Length Palindromic Substrings                                                                      
                                                                                                                       
                                                                                                                       
    INPUT                                                                                                              
    =====                                                                                                              
                                                                                                                       
    %let keyword=AYUSH;                                                                                                
                                                                                                                       
    options validvarname=upcase;                                                                                       
    libname sd1 "d:/sd1";                                                                                              
    data sd1.have;                                                                                                     
     input words$;                                                                                                     
    cards4;                                                                                                            
    STAT                                                                                                               
    MATH                                                                                                               
    HISTORY                                                                                                            
    POLYSCI                                                                                                            
    ;;;;                                                                                                               
    run;quit;                                                                                                          
                                                                                                                       
     SD1.HAVE total obs=4                                                                                              
                                                                                                                       
       WORDS                                                                                                           
                                                                                                                       
       STAT                                                                                                            
       MATH                                                                                                            
       HISTORY                                                                                                         
       POLYSCI                                                                                                         
                                                                                                                       
    EXAMPLE OUTPUT                                                                                                     
    --------------                                                                                                     
                                                                                                                       
    CAESAR CIPHER                                                                                                      
                                                                                                                       
    WORK.MDATA total obs=4                                                                                             
                                                                                                                       
      INDEX    WORDS      WORDL    ENCRYPT    DECRYPT                                                                  
                                                                                                                       
        0      STAT         4      WXEX       STAT                                                                     
        1      MATH         4      QEXL       MATH                                                                     
        2      HISTORY      7      OPZAVYF    HISTORY                                                                  
        3      POLYSCI      7      WVSFZJP    POLYSCI                                                                  
                                                                                                                       
    VIGENÈRE CIPHER                                                                                                    
                                                                                                                       
                                                                                                                       
    WORK.MDATA total obs=4                                                                                             
                                                                                                                       
      INDEX    WORDS      WORDL    VENCRYPT    VDECRYPT                                                                
                                                                                                                       
        0      STAT         4      SRUL        STAT                                                                    
        1      MATH         4      MYNZ        MATH                                                                    
        2      HISTORY      7      HGMLVRW     HISTORY                                                                 
        3      POLYSCI      7      PMFQZCG     POLYSCI                                                                 
                                                                                                                       
                                                                                                                       
    PROCESS                                                                                                            
    =======                                                                                                            
                                                                                                                       
    1  Caesar Cipher   https://www.geeksforgeeks.org/caesar-cipher/                                                    
    ---------------------------------------------------------------                                                    
                                                                                                                       
                                                                                                                       
    %utl_submit_py64("                                                                                                 
    import numpy as np;                                                                                                
    import pandas as pd;                                                                                               
    from sas7bdat import SAS7BDAT;                                                                                     
    with SAS7BDAT('d:/sd1/have.sas7bdat') as m:;                                                                       
    .   mdata = m.to_data_frame();                                                                                     
    .   mdata['WORDL'] = mdata['WORDS'].apply(len);                                                                    
    .   mdata['ENCRYPT'] = mdata['WORDS'];                                                                             
    .   mdata['DECRYPT'] = mdata['WORDS'];                                                                             
    .   print(mdata);                                                                                                  
    .   mdata.info();                                                                                                  
    .   print(range(len(mdata)));                                                                                      
    def encrypt(text,s):;                                                                                              
    .   result = '';                                                                                                   
    .   for i in range(len(text)):;                                                                                    
    .       char = text[i];                                                                                            
    .       if (char.isupper()):;                                                                                      
    .           result += chr((ord(char) + s-65) % 26 + 65);                                                           
    .       else:;                                                                                                     
    .           result += chr((ord(char) + s - 97) % 26 + 97);                                                         
    .   return result;                                                                                                 
    for i in range(len(mdata)):;                                                                                       
    .   text=mdata.iat[i, 0];                                                                                          
    .   s=mdata.iat[i, 1];                                                                                             
    .   print (text);                                                                                                  
    .   print(s);                                                                                                      
    .   print 'Cipher: ' + encrypt(text,s);                                                                            
    .   mdata.at[i, 'ENCRYPT'] = encrypt(text,s);                                                                      
    .   mdata.at[i, 'DECRYPT'] = encrypt(encrypt(text,s),26-s);                                                        
    mdata.to_stata('d:/dta/encrypt.dta');                                                                              
    ");                                                                                                                
                                                                                                                       
    filename imp 'd:/dta/encrypt.dta' lrecl=32756;                                                                     
    proc import                                                                                                        
       out=work.mdata                                                                                                  
       file=imp                                                                                                        
       dbms=DTA replace;                                                                                               
    run;                                                                                                               
                                                                                                                       
    proc print data=mdata;                                                                                             
    run;quit;                                                                                                          
                                                                                                                       
                                                                                                                       
    2  Vigenère Cipher https://www.geeksforgeeks.org/vigenere-cipher/                                                  
    -----------------------------------------------------------------                                                  
                                                                                                                       
    %let keyword=AYUSH;                                                                                                
                                                                                                                       
    %utl_submit_py64("                                                                                                 
    import numpy as np;                                                                                                
    import pandas as pd;                                                                                               
    from sas7bdat import SAS7BDAT;                                                                                     
    with SAS7BDAT('d:/sd1/have.sas7bdat') as m:;                                                                       
    .   mdata = m.to_data_frame();                                                                                     
    .   mdata['WORDL'] = mdata['WORDS'].apply(len);                                                                    
    .   mdata['VENCRYPT'] = mdata['WORDS'];                                                                            
    .   mdata['VDECRYPT'] = mdata['WORDS'];                                                                            
    .   print(mdata);                                                                                                  
    .   mdata.info();                                                                                                  
    .   print(range(len(mdata)));                                                                                      
    def generateKey(string, key):;                                                                                     
    .   key = list(key);                                                                                               
    .   if len(string) == len(key):;                                                                                   
    .       return(key);                                                                                               
    .   else:;                                                                                                         
    .       for i in range(len(string) -;                                                                              
    .                      len(key)):;                                                                                 
    .           key.append(key[i % len(key)]);                                                                         
    .   return('' . join(key));                                                                                        
    def cipherText(string, key):;                                                                                      
    .   cipher_text = [];                                                                                              
    .   for i in range(len(string)):;                                                                                  
    .       x = (ord(string[i]) +;                                                                                     
    .            ord(key[i])) % 26;                                                                                    
    .       x += ord('A');                                                                                             
    .       cipher_text.append(chr(x));                                                                                
    .   return('' . join(cipher_text));                                                                                
    def originalText(cipher_text, key):;                                                                               
    .   orig_text = [];                                                                                                
    .   for i in range(len(cipher_text)):;                                                                             
    .       x = (ord(cipher_text[i]) -;                                                                                
    .            ord(key[i]) + 26) % 26;                                                                               
    .       x += ord('A');                                                                                             
    .       orig_text.append(chr(x));                                                                                  
    .   return('' . join(orig_text));                                                                                  
    if __name__ == '__main__':;                                                                                        
    .   for i in range(len(mdata)):;                                                                                   
    .       keyword = '&keyword';                                                                                      
    .       text=mdata.iat[i, 0];                                                                                      
    .       s=mdata.iat[i, 1];                                                                                         
    .       print (text);                                                                                              
    .       print(s);                                                                                                  
    .       key = generateKey(text, keyword);                                                                          
    .       cipher_text = cipherText(text,key);                                                                        
    .       print('Ciphertext :', cipher_text);                                                                        
    .       print('Original/Decrypted Text :',originalText(cipher_text, key));                                         
    .       mdata.at[i, 'VENCRYPT'] = cipher_text;                                                                     
    .       mdata.at[i, 'VDECRYPT'] = originalText(cipher_text, key);                                                  
    mdata.to_stata('d:/dta/vigenere.dta');                                                                             
    ");                                                                                                                
                                                                                                                       
    filename imp 'd:/dta/vigenere.dta' lrecl=32756;                                                                    
    proc import                                                                                                        
       out=work.mdata                                                                                                  
       file=imp                                                                                                        
       dbms=DTA replace;                                                                                               
    run;                                                                                                               
                                                                                                                       
    proc print data=mdata;                                                                                             
    run;quit;                                                                                                          
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
                                                                                                                       
