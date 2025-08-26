# enlazado_4.5
Código y resultados

1. Datos

Para este primer experimento se han usado como base la Labour Law Terminology (https://zenodo.org/records/3843561). El conjunto de datos contiene más de 700 términos del ámbito del derecho laboral español. Para cada término, se han recopilado traducciones al inglés, alemán y neerlandés, así como sinónimos y definiciones, a partir de recursos de la nube de Linguistic Linked Open Data (como Wikidata y Eurovoc), además de otras fuentes terminológicas como IATE. El conjunto total de datos se denomina labourlawterminologyv1.nt dentro de la carpeta que contiene todos los documentos. Para los experimentos de este trabajo, se extrajeron las tripletas entre términos de la propia terminología y términos de Eurovoc, siendo un total de 187 enlaces entre términos, todos ellos de naturaleza exactMatch, se pueden ver en el archivo llamado tripletas_uris.nt, y las mismas tripletas pero solo con sus formas literales se encuentran en el archivo tripletas_convertidas.nt. El código empleado para la extracción y procesamiento de estas tripletas se denomina extracción_enlaces.ipynb. 

A su vez, estos términos se han proyectado sobre el documento del Estatuto de los Trabajadores (2015), ya que muchos de ellos se han extraído de esa fuente, aunque no todos. Por ello, aquellos términos que no se encuentran en los estatutos se han eliminado, quedando finalmente 64 enlaces. El texto del Estatuto de los Trabajadores aparece dividido por artículos y párrafos en la carpeta llamada files. Después de ese primer preprocesado, se han dividido los términos de la terminología Labour Law y de Eurovoc en los archivos: labour_law_literales.txt y eurovoc_literales.txt. Tras ello, se han proyectado los términos del archivo labour_law_literales.txt a través de todos los artículos de los estatutos y se han extraído todas sus apariciones. El código para ello es el denominado contextos_estatutos.ipynb. Las apariciones están formadas por las 20 palabras previas al término y todas las palabras posteriores hasta el primer punto que aparezca. Los términos junto a sus contextos se encuentran en el documento llamado terminos_contextos.csv. 


3. Experimentos generación de contexto

Tras haber extraído todos los contextos de cada término, se presupone que al tratarse de un corpus de dominio tan específico, se puede determinar que cada término cuenta con el significado más relevante en dicho corpus:
   
    A. google/flan-t5-base, el notebook que contiene el código es generación_contextos_flan_falcon_llama8b.ipynb
    
    B. tiiuae/falcon-rw-1b, el notebook que contiene el código es generación_contextos_flan_falcon_llama8b.ipynb
    
    C. meta-llama/Llama-3.2-1B, el notebook que contiene el código es generación_contextos_llama1b.ipynb
    
    D. nvidia/Llama-3.1-Nemotron-Nano-8B-v1, el notebook que contiene el código es generación_contextos_flan_falcon_llama8b.ipynb
    
    E. meta-llama/Llama-3.1-8B-Instruct, el notebook que contiene el código es generación_contextos.ipynb para los términos del documento de los Estatutos y generación_contextos-eurovoc.ipynb para los términos de Eurovoc. 


Los archivos con las ventanas de contexto generadas se denominan mediante zero-shot prompting:

    A. Flan-t5-base: terminos_ventanas_contexto_flan.csv
    
    B. Falcon-rw-1b: terminos_ventanas_contexto_falcon.csv
    
    C. Llama-3.2-1B: terminos_ventanas_contexto_llama1b.csv
    
    D. Llama-3.1-Nemotron-Nano-8B-v1: terminos_ventana_contexto_llama8b.csv

    E. Llama-3.1-8B-Instruct: terminos_inst_1shot_limpio.csv para los términos del documento de los Estatutos y eurovoc_inst_3shot_limpio.csv para los términos de Eurovoc.


5. Experimentos enlazado de términos

     A. Embeddings:
   
           - ROBERTA: RoBERTa_labourlaw.ipynb
   
           - BERT: Bert_labour_law.ipynb
   
           - Universal Sentence Encoder: universal_sentence_encoder_labour_law.ipynb

     B. LLMs: el código se encuentra en el notebook llamado enlazado_LLaMA3.ipynb. Los archivos juntos a los enlaces detectados mediante prompting son: enlaces_detectados.ipynb, enlaces_detectados_one_shot.ipynb y enlaces_detectados_two_shot.ipynb

   


