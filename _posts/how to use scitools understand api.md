# scitools understand api 使用

---

layout: post
title: "how to use scitools understand api"
date: 2025-04-23
toc: false
tags: [Debug]

---

read the official tutorials listed below:

https://support.scitools.com/support/solutions/folders/70000470852

# set the correct und execution path

1. run the und

```bash
/home/caesar/.local/share/understand/bin/linux64/und 
```

1. create the db and then add the repo to be analyzed in it
    1. Use the und create command to create a new project. Specify the name of the project either with the -db option or as the last parameter. Any settings allowed with the settings command (see page 352) can also be used with create. For example:
        
        ```bash
        
        /home/caesar/.local/share/understand/bin/linux64/und create -db /home/caesar/caesar/Diasplus/dataset_construction/use_understand_to_analyze_call_graph/data/pandas.und -languages python
        ```
        
    2. If you have a small number of source files then it may be easiest to just supply their names to the analyzer using the wildcard abilities of your operating system shell. For example:
        
        ```bash
        /home/caesar/.local/share/understand/bin/linux64/und -db /home/caesar/caesar/Diasplus/dataset_construction/use_understand_to_analyze_call_graph/data/pandas.und add /home/caesar/caesar/Diasplus/dataset_construction/use_understand_to_analyze_call_graph/data/pandas/pandas
        ```
        
2. use the und python interpreter
    
    ```bash
    /home/caesar/.local/share/understand/bin/linux64/Python/bin/python3.13
    ```
    
    or you can specify the interpreter in the terminal to avoid declare it in the sh file every time
    
    ```bash
    alias python="/home/caesar/.local/share/understand/bin/linux64/Python/bin/python3.13"
    ```
    
3. refer to the api doc to check how to use api 
    1. https://docs.scitools.com/manuals/python/genindex.html