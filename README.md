# Análise de currículos usando NLP e Web Scraping

### Aluno: [Elio Accardo](https://github.com/ElioAccardo) 
### Orientador: [Leonardo Mendoza].
### Co-orientador: [Felipe Borges](https://github.com/FelipeBorgesC).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

---

### Resumo 

Este projeto tem como objetivo fornecer soluções para pessoas que procuram receber feedback sobre seus currículos, bem como para equipes de Recursos Humanos que querem comparar candidatos para posições específicas. O projeto foi desenvolvido pensando na solução do CV WAY (http://www.gocvway.com/index).

O projeto é dividido em três etapas:

- Análise de currículos com a mesma experiência profissional: O código em Python procura no banco de dados currículos com a mesma experiência profissional. Em seguida, ele monta um currículo ideal com base na pontuação das frases e, por fim, compara a similaridade entre os currículos e o currículo ideal usando a similaridade de cossenos.

- Web Scraping: Com base nas possíveis combinações de trabalhos alvo, o código procura descrições de vagas.

- Análise de currículos com o mesmo trabalho alvo: O código procura por currículos no banco de dados e, com base nas descrições de vagas obtidas na segunda etapa, compara os currículos com o mesmo interesse em posições usando a similaridade de cossenos.


### Abstract 

This work consists of a solution for people who want to get feedback on their resumes, as well as for HR teams who want to compare candidates for specific positions. The project developed is a solution from an initiative called CV WAY (http://www.gocvway.com/index)

The work is divided into 3 steps:

- Analysis of resumes with the same work experience: The Python code searches the database for resumes with the same professional experience. Then it builds an ideal resume based on the score of the phrases and finally compares the similarity between the resumes and the ideal resume using cosine similarity.

- Web Scraping: Based on possible combinations of target job, the code searches for job descriptions.

- Analysis of resumes with the same target job: The code searches for resumes in the database and based on the job descriptions obtained in the previous step, it compares the resumes with the same interest in positions using cosine similarity.
    
### 1. Introdução 

O projeto desenvolvido é uma iniciativa para melhorar a solução da plataforma CV WAY.

A plataforma CV WAY é uma ferramenta que profissionais podem usar para aprimorar seus currículos por meio da troca de revisões. Ao correspondê-lo com outros usuários experientes nas indústrias e funções que você pretende atuar.

Antes, a plataforma CV WAY dependia da avaliação de outros usuários experientes para que você tivesse acesso a um painel pessoal. Com o desenvolvimento deste projeto, os usuários da plataforma poderão receber feedback imediato sobre seus currículos, permitindo-lhes saber quanto é competitivo seu perfil por meio da classificação com outros candidatos.

### 2. Modelagem

1) Código em python NLP: Análise dos currículos com mesmo work experience (rank).

- Importar texto dos currículos via SQL através do pacote ”sqlalchemy”;
- Limpar texto dividido em frases (separar work experience e education);
- Remover palavras de parada (stop-words);
- Classificar frases: Rankear as frases com base nas pontuações;
- Selecionar as principais N frases para resumo;
- Montar CV Ideal juntando work experience e education;
- Calcular similaridade usando TF_IDF e Rankear os currículos;
- Insert do dataframe no banco dados MYSQL (”pandas.to_sql”).


2) Web Scraping: Com base no target job de cada currículo, buscar a descrição de vagas.

- Pré-trabalho:
    - Site utilizado para o scraping: Indeed;
    - Traduzir os target jobs da plataforma para palavras chave de busca no indeed;
    - Separar lista de links do indeed e palavras chave para a descrição das vagas.
- Scraping:
    - Estrutura de repetição para acessar a lista de links; 
    - Aprovação de cookies (tentativa e exceção);
    - Procurar uma vaga de emprego através das palavras chave;
    - Remover popup de alerta de trabalho (bloqueio do scraping) - tentativa e exceção;
    - Buscar os 3 primeiros cartões de descrição de vagas;
    - Consolidar em um dataframe.
- Exportar dados:
    - Insert do dataframe no banco dados MYSQL (”pandas.to_sql”);
    - Exportação do dataframe para .csv.

3) Código em python NLP: Análise dos currículos com mesmo target job (rank).

- Importar texto dos currículos via SQL através do pacote ”sqlalchemy”;
- Limpar texto dos currículos;
- Remover palavras de parada (stop-words);
- Importar texto da etapa de web scraping;
- Limpar texto do web scraping;
- Para cada target job comparar os currículos e classificá-los (rankear) usando TF_IDF;
- Insert do dataframe no banco dados MYSQL (”pandas.to_sql”).

### 3. Resultados 

1) Código em python NLP para análise dos currículos com mesmo work experience.

- Work Experience (departamento/industria/senioridade): Customer Service/Food, drink, tobacco/Middle
- CVs: 

    * CV1: Classification (TF_IDF)=0.23945600613050613/Rank=3

        WORK EXP

        COMPANY NAME: Coffee planet.
        JOB TITLE: Barista.
        DESCRIPTION:

        EDUCATION

        TYPE: HIGHSCHOOL.
        INSTITUITION NAME: Peak solution school.
        DEGREE PROGRAM: Metric.
        DESCRIPTION:

        TYPE: COLLEGEUNIVERSITY,.
        INSTITUITION NAME: Punjab college.
        DEGREE PROGRAM: Intermediate.
        DESCRIPTION:

    * CV2: Classification (TF_IDF)=0.5885295041149788/Rank=2

        WORK EXP

        COMPANY NAME: Pizza Hut.
        JOB TITLE: Waiter.
        DESCRIPTION: Worked passionately in customer service in a high-volume restaurant. Completed the F.A.S.T. customer service training class. Maintained a high tip         average thanks to consistent customer satisfaction.

        EDUCATION

        TYPE: COLLEGEUNIVERSITY,.
        INSTITUITION NAME: Hubei university of technology.
        DEGREE PROGRAM: Bachelor in computer science.
        DESCRIPTION: Studied with outstanding cgpa in this university

        TYPE: MASTER.
        INSTITUITION NAME: Wuhan University.
        DEGREE PROGRAM: Masters in computer science.
        DESCRIPTION: Studying masters under this university

    * CV3: Classification (TF_IDF)=0.7084409562684878/Rank=1

        WORK EXP

        COMPANY NAME: Meet Fresh.
        JOB TITLE: accountant.
        DESCRIPTION: I was working in meet fresh as a accountant, I''m specialist in account manager, I hold all the account department charge .

        EDUCATION

        TYPE: COLLEGEUNIVERSITY,.
        INSTITUITION NAME: University of Western Australia.
        DEGREE PROGRAM: BSc .
        DESCRIPTION: i do BSc in science subject from from university of western Australia

        TYPE: MASTER,.
        INSTITUITION NAME: University of Tasmania.
        DEGREE PROGRAM: MSc.
        DESCRIPTION: i do Masters in science subject from from university of Tasmania

2) Web Scraping e código em python NLP para análise dos currículos com mesmo target job.

- Target Job (departamento/industria/senioridade): Human Resources/Agriculture/Intern
- Palavra chave no web scraping: Human Resources, Intern
- Job Description (Web Scraping):

    * Job Description 1 (Scraping):

        list 4-5 requirements: software/technology experience, education requirements (if any), years of experience, etc.]
        Cerence Inc. (Nasdaq: CRNC and www.cerence.com) is the global industry leader in creating unique, moving experiences for the automotive world. Spun out from           Nuance in October 2019, Cerence is a new, independent company that has quickly gained traction as a leader in the automotive voice assistant space, working             with all of the world’s leading automakers – from Ford and Fiat Chrysler to Daimler, Audi and BMW to Geely and SAIC – to transform how a car feels, responds           and learns. Its track record is built on more than 20 years of industry experience and leadership and more than 325 million cars on the road today across more         than 70 languages.

        As Cerence looks to the future and continues an ambitious growth agenda, we need someone to join the team and help build the future of voice and AI in cars.           This is an exciting opportunity to join Cerence’s passionate, dedicated, global team and be a part of meaningful innovation in a rapidly growing industry.
        EQUAL OPPORTUNITY EMPLOYER
        Cerence is firmly committed to Equal Employment Opportunity (EEO) and to compliance with all federal, state and local laws that prohibit employment                     discrimination on the basis of age, race, color, gender, gender identity, gender expression, sex, sex stereotyping, pregnancy, national origin, ancestry,               religion, physical or mental disability, medical condition, marital status, citizenship status, sexual orientation, protected military or veteran status,               genetic information and other protected classifications. Cerence Equal Employment Opportunity Policy Statement.
        All prospective and current Employees need to remain vigilant when it comes to executing security policies in the workplace. This includes:

        Following workplace security protocols and training programs to familiarize with the ways to maintain a safe workplace.
        Following security procedures to report any suspicious activity.
        Having respect for corporate security procedures to allow those procedures to be effective.
        Adhering to company's compliance and regulations.
        Encouraging to follow a zero tolerance for workplace violence.
        Basic knowledge of information security and data privacy requirements (e.g., how to protect data & how to be handling this data).
        Demonstrative knowledge of information security through internal training programs.

    * Job Description 2 (Scraping):

        We are looking for a Data Scientist who will support our product, sales, leadership and marketing teams with insights gained from analyzing company data. The           ideal candidate is adept at using large data sets to find opportunities for product and process optimization and using models to test the effectiveness of             different courses of action.
        They must have strong experience using a variety of data mining/data analysis methods, using a variety of data tools, building and implementing models,                 using/creating algorithms and creating/running simulations. They must have a proven ability to drive business results with their data-based insights.
        They must be comfortable working with a wide range of stakeholders and functional teams. The right candidate will have a passion for discovering solutions             hidden in large data sets and working with stakeholders to improve business outcomes.

        Skills
        DB2 Java Python C++ C MySQL R JavaScript
        Responsibilities
        Work with stakeholders throughout the organization to identify opportunities for leveraging company data to drive business solutions.
        Mine and analyze data from company databases to drive optimization and improvement of product development, marketing techniques and business strategies.
        Assess the effectiveness and accuracy of new data sources and data gathering techniques.
        Develop custom data models and algorithms to apply to data sets.
        Use predictive modeling to increase and optimize customer experiences, revenue generation, ad targeting and other business outcomes.
        Develop company A/B testing framework and test model quality.
        Coordinate with different functional teams to implement models and monitor outcomes.
        Develop processes and tools to monitor and analyze model performance and data accuracy.
        Job Summary 
        Offered Salary
        No
        Career Level
        Internship
        Experience
        Fresher
        Qualification
        MCA M.Tech (CSE/IT/ECE/ME)

- CVs: 

    * CV1: Classification (TF_IDF)= 0,007297923313080487/Rank=3

        WORK EXP:

        EDUCATION:
        TYPE: COLLEGE UNIVERSITY,.
        INSTITUITION NAME: kavindu.
        DEGREE PROGRAM: english.
        DESCRIPTION:

    * CV2: Classification (TF_IDF)=0,05208210211224387/Rank=2

        WORK EXP

        COMPANY NAME: Zoom.
        JOB TITLE: Intern.
        DESCRIPTION: Worked at zoom.

        COMPANY NAME: Microsoft.
        JOB TITLE: Intern.
        DESCRIPTION: Was the Marketing Intern.

        COMPANY NAME: Amazon.
        JOB TITLE: Virtual Assistant.
        DESCRIPTION: Was the Virtual Assistant for different comapanies in Amazon.

        EDUCATION

        TYPE: COLLEGEUNIVERSITY,.
        INSTITUITION NAME: Harvard.
        DEGREE PROGRAM: Bachelors in Marketing.
        DESCRIPTION: Studied at Harvard

        TYPE: MASTER.
        INSTITUITION NAME: University of Dundee.
        DEGREE PROGRAM: Masters in Marketing.
        DESCRIPTION: Studied at Dundee Uk

* CV3: Classification (TF_IDF)=0,12545522138105042/Rank=1


### 4. Conclusões

Conclui-se que o trabalho atingiu seu objetivo de melhorar a solução existente do CV WAY. Em questão de poucos minutos, foi possível classificar todo o banco de dados com base em dois critérios distintos.

A etapa de web scraping também foi satisfatória, pois varreu mais de 115 combinações de posições-alvo e permitiu a classificação dos currículos comparando as palavras-chave de posições diferentes.

Como oportunidades de melhoria identificadas estão:

- Refatoração do código de web scraping para melhor mapeamento de gargalos e otimizar o tempo do Selenium;
- Refatoração do código de NLP para otimizar consultas;
- Deploy do código em produção.

--- 

Matrícula: 211.101.170

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master* 
