configuração do prodigy

/home/apereira/.prodigy/

{
        "port": 8050,
        "host": "0.0.0.0",
        "instructions": "./prodigy/data/instructions/instructions.html",
        "ui_lang": "pt"

}


prodigy ner.correct vida_funcional pt_core_news_sm ./prodigy/data/vida_funcional_all.jsonl --label NOME,CPF,CARGO,RG,PROCESSO_ADM

prodigy train ./prodigy/model/vida_funcional_model --ner vida_funcional

prodigy ner.teach vida_funcional_corrigido_v1 ./prodigy/model/vida_funcional_model/model-last/ ./prodigy/data/vida_funcional_all.jsonl --label NOME,CPF,CARGO,RG,PROCESSO_ADM

prodigy ner.silver-to-gold vida_funcional vida_funcional_corrigido_v1 ./prodigy/model/vida_funcional_model/model-last/

prodigy ner.correct vida_funcional ./prodigy/model/vida_funcional_model/model-last/ ./prodigy/data/vida_funcional_all.jsonl --label NOME,CPF,CARGO,RG,PROCESSO_ADM