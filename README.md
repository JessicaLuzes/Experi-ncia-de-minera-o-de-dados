# Experiência de mineração de dados em avaliação ex-post de políticas na área da cultura - Proposta UFRJ/2020 - Comemoração dos 100 anos da UFRJ

Primeiro Script
install.packages("tm")
library(tm)
library(NLP)
# testando a identificação de arquivos
docs <- c("nome do primeiro arquivo", "nome do segundo arquivo")
Texto <- VCorpus(VectorSource(docs))

Segundo script
#Carregando todos os arquivos em um único arquivo
library(tm)
setwd("/cloud/project/**nome da pasta onde se encontram os arquivos**)
arquivotxt <- c("/cloud/project/**nome da pasta onde se encontram os arquivos**")
textos <- VCorpus(DirSource(arquivotxt, encoding = "UTF-8"),readerControl = list(language = "lat"))
VCorpus(VectorSource(textos))


# inspecionando os arquivos
inspect(textos[1:2])

# identificando os textos
meta(textos[[1]], "id")
meta(textos[[2]], "id")

#visualizando os dados
inspect(textos[[1]])
inspect(textos[[2]])

#Visualizacao dos dados informando quantidade de linhas
lapply(textos[1:2], as.character)

#####################################
#        TRANSFORMACOES             #
#####################################

# Retirando os espaços em branco
textostrans <- tm_map(textos, stripWhitespace)
inspect(textostrans[[1]])

# Transformando todos os caracteres para minúsculo, para uniformizar
textostrans  <- tm_map(textostrans, content_transformer(tolower))
inspect(textostrans[[1]])

# utilizando o arquivo de stowords
stopwords("pt")
textostrans <- tm_map(textostrans, removeWords, stopwords("pt"))
inspect(textostrans[[1]])
inspect(textostrans[[2]])

# acrescentando mais stopwords
stopwords_pt <- c(stopwords("pt"), "presidente", "é", "sr", "sra","irá")
textostrans <- tm_map(textostrans, removeWords, stopwords_pt)
inspect(textostrans[[1]])
inspect(textostrans[[2]])
