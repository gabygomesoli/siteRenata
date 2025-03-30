<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Estante de Livros com Carrossel</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(120deg, #84fab0, #8fd3f4);
            min-height: 100vh;
        }
        .main-container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        }
        h1 {
            color: #333;
            text-align: center;
            margin-bottom: 30px;
            font-size: 2.5rem;
        }
        .search-container {
            margin-bottom: 30px;
        }
        #search {
            width: 100%;
            padding: 15px;
            border: 2px solid #8fd3f4;
            border-radius: 10px;
            font-size: 18px;
            outline: none;
            transition: all 0.3s;
        }
        #search:focus {
            border-color: #84fab0;
            box-shadow: 0 0 10px rgba(132, 250, 176, 0.5);
        }
        .carousel-container {
            margin-bottom: 40px;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15);
        }
        .carousel-item img {
            height: 500px;
            object-fit: contain;
            background-color: #f8f9fa;
        }
        .carousel-caption {
            background-color: rgba(0, 0, 0, 0.7);
            border-radius: 8px;
            padding: 15px;
            bottom: 20px;
        }
        .book-title {
            font-weight: bold;
            font-size: 1.4rem;
            color: #fff;
        }
        .book-author {
            font-style: italic;
            color: #ddd;
        }
        .book-list {
            list-style: none;
            padding: 0;
            margin-top: 30px;
        }
        .book-list li {
            padding: 15px;
            border-bottom: 1px solid #eee;
            font-size: 18px;
            background: #f9f9f9;
            transition: all 0.3s;
            border-radius: 8px;
            margin: 8px 0;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .book-list li:hover {
            background: #8fd3f4;
            color: white;
            transform: translateX(5px);
        }
        .book-details {
            display: none;
            background: #f1f1f1;
            padding: 15px;
            border-radius: 8px;
            margin-top: 10px;
            text-align: left;
            color: #333;
        }
        .flag-icon {
            width: 24px;
            height: 16px;
            margin-left: 10px;
            border: 1px solid #ddd;
        }
        .no-results {
            text-align: center;
            padding: 20px;
            font-size: 18px;
            color: #666;
        }
        .translate-btn {
            background-color: #84fab0;
            color: #333;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            margin-top: 10px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
        }
        .translate-btn:hover {
            background-color: #6ad89c;
        }
        @media (max-width: 768px) {
            .carousel-item img {
                height: 300px;
            }
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <h1>📚 Estante de Livros com Carrossel 📖</h1>
        
        <div class="search-container">
            <input type="text" id="search" placeholder="🔍 Pesquisar livros por título ou autor...">
        </div>
        
        <div class="carousel-container">
            <div id="bookCarousel" class="carousel slide" data-bs-ride="carousel">
                <div class="carousel-indicators">
                    <!-- Os indicadores serão adicionados pelo JavaScript -->
                </div>
                
                <div class="carousel-inner">
                    <!-- Os itens do carrossel serão adicionados pelo JavaScript -->
                </div>
                
                <button class="carousel-control-prev" type="button" data-bs-target="#bookCarousel" data-bs-slide="prev">
                    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Anterior</span>
                </button>
                <button class="carousel-control-next" type="button" data-bs-target="#bookCarousel" data-bs-slide="next">
                    <span class="carousel-control-next-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Próximo</span>
                </button>
            </div>
        </div>
        
        <h2>Lista Completa de Livros</h2>
        <ul id="books" class="book-list"></ul>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        const books = [
            { title: "Cartas Sertanejas Professarias", author: "Júlio Ribeiro", nationality: "br", 
              details: "Este livro narra as experiências e cartas de um professor no sertão.", 
              details_en: "This book narrates the experiences and letters of a teacher in the backlands.",
              image: "https://m.media-amazon.com/images/I/81keheswvoL.jpg" },
            
            { title: "Triste Fim de Policarpo Quaresma", author: "Lima Barreto", nationality: "br", 
              details: "Uma crítica social sobre o Brasil pós-abolição e seus desafios.", 
              details_en: "A social critique about post-abolition Brazil and its challenges.",
              image: "https://m.media-amazon.com/images/I/71e5C8gV19L._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "O Cortiço em Cordel", author: "Aluísio de Azevedo", nationality: "br", 
              details: "A obra descreve a vida nos cortiços, com foco em problemas sociais e humanos.", 
              details_en: "The work describes life in tenements, focusing on social and human problems.",
              image: "https://m.media-amazon.com/images/I/81y1nZheSFL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "Inovação", author: "Renato Cruz", nationality: "br", 
              details: "Focado em temas contemporâneos, o livro explora o conceito de inovação no Brasil.", 
              details_en: "Focused on contemporary themes, the book explores the concept of innovation in Brazil.",
              image: "https://m.media-amazon.com/images/I/61HI6z3FekL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "A Muralha", author: "Diná Silveira de Queiroz", nationality: "br", 
              details: "Um romance que trata de relações humanas, conflitos e identidade.", 
              details_en: "A novel that deals with human relationships, conflicts and identity.",
              image: "https://m.media-amazon.com/images/I/91zrafbcgJS.jpg" },
            
            { title: "O Seminarista", author: "Bernardo Guimarães", nationality: "br", 
              details: "A história de um seminarista que se perde em dilemas de fé e amor.", 
              details_en: "The story of a seminarian who gets lost in dilemmas of faith and love.",
              image: "https://m.media-amazon.com/images/I/61ggTTE+deL.jpg" },
            
            { title: "Divã", author: "Martha Medeiros", nationality: "br", 
              details: "Uma obra que mistura ficção e reflexão sobre a vida moderna e as relações.", 
              details_en: "A work that mixes fiction and reflection on modern life and relationships.",
              image: "https://m.media-amazon.com/images/I/81QY+k7uIjL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "Contar Histórias", author: "Fábiano Moraes", nationality: "br", 
              details: "Uma obra que resgata a tradição oral e as histórias contadas ao longo do tempo.", 
              details_en: "A work that rescues oral tradition and stories told over time.",
              image: "https://encrypted-tbn2.gstatic.com/shopping?q=tbn:ANd9GcT5e6DJI57tTu2x9l571hcjaaZMG-f_t-ShTVLqTN6msJp_0WVfZunaPYu7mO5raUX5nM928Nh1KVJjGlLAmXI1glJ69A5-vQPnTWjB44EHDhMyH0wQs9Q7" },
            
            { title: "Madrugada sem Deus", author: "Mário Donato", nationality: "br", 
              details: "Relatos de uma vida marcada pela solidão e pela busca por sentido.", 
              details_en: "Accounts of a life marked by loneliness and the search for meaning.",
              image: "https://m.media-amazon.com/images/I/61MPMY51AXL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "Cabo de Guerra", author: "Ivone Benedetti", nationality: "br", 
              details: "Uma análise das relações humanas em tempos de tensão e conflito.", 
              details_en: "An analysis of human relationships in times of tension and conflict.",
              image: "https://m.media-amazon.com/images/I/71K6EIYTl-L._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "Um Olhar que Transforma", author: "Januário Cristina Alves", nationality: "br", 
              details: "O livro propõe reflexões sobre o mundo do trabalho e suas diversas faces.", 
              details_en: "The book proposes reflections on the world of work and its various aspects.",
              image: "https://down-br.img.susercontent.com/file/sg-11134201-7rfhk-m39u5m2elhsn54" },
            
            { title: "Memórias Inventadas", author: "Manoel de Barros", nationality: "br", 
              details: "Uma narrativa sobre infância e a memória inventada do autor.", 
              details_en: "A narrative about childhood and the author's invented memory.",
              image: "https://m.media-amazon.com/images/I/91q-O8+8bOL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "Fogo Morto", author: "José Lins do Rego", nationality: "br", 
              details: "Romance que descreve o interior nordestino e seus conflitos.", 
              details_en: "Novel that describes the northeastern countryside and its conflicts.",
              image: "https://m.media-amazon.com/images/I/81UlUUgB3tL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "A Droga da Obediência", author: "Pedro Bandeira", nationality: "br", 
              details: "Uma obra infantojuvenil que mistura ação e reflexão sobre a obediência.", 
              details_en: "A youth book that mixes action and reflection on obedience.",
              image: "https://m.media-amazon.com/images/I/91nzO719GpL.jpg" },
            
            { title: "Monteiro Lobato: O Editor do Brasil", author: "Cassiano Nunes", nationality: "br", 
              details: "Uma biografia de Monteiro Lobato e seu impacto no Brasil.", 
              details_en: "A biography of Monteiro Lobato and his impact on Brazil.",
              image: "https://m.media-amazon.com/images/I/91UHQSN2vgL.jpg" },
            
            { title: "O Cabeleira", author: "Franklin Távora", nationality: "br", 
              details: "Um romance que aborda a vida no sertão e a luta contra as injustiças.", 
              details_en: "A novel that addresses life in the backlands and the fight against injustices.",
              image: "https://m.media-amazon.com/images/I/81Ehk8ESqXS._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "O Outro Apaixonado por Marília de Dirceu", author: "Jair Vitória", nationality: "br", 
              details: "A obra descreve um amor impossível entre os personagens.", 
              details_en: "The work describes an impossible love between the characters.",
              image: "https://m.media-amazon.com/images/I/91b+eajkWbL.jpg" },
            
            
            { title: "O Zahir", author: "Paulo Coelho", nationality: "br", 
              details: "Explora o conceito do 'Zahir', algo que não pode ser ignorado na vida.", 
              details_en: "Explores the concept of 'Zahir', something that cannot be ignored in life.",
              image: "https://m.media-amazon.com/images/I/81OA9y6fDUL._UF894,1000_QL80_.jpg" },
            
            { title: "Espumas Flutuantes", author: "Castro Alves", nationality: "br", 
              details: "Poemas que exploram a liberdade e os direitos humanos.", 
              details_en: "Poems that explore freedom and human rights.",
              image: "https://m.media-amazon.com/images/I/51HDZ2ITqhL._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "A Perfeição", author: "Eça de Queiroz", nationality: "pt", 
              details: "Uma crítica social que aborda a busca pela perfeição na sociedade.", 
              details_en: "A social critique that addresses the pursuit of perfection in society.",
              image: "https://cdn.kobo.com/book-images/85e84ece-bf24-4a93-9ab0-10a6dbda3eea/1200/1200/False/a-perfeicao.jpg" },
            
            { title: "Gaivota / Tio Vânia", author: "Anton Tchekhov", nationality: "ru", 
              details: "Duas peças que tratam do dilema existencial e da busca por significado.", 
              details_en: "Two plays that deal with existential dilemma and the search for meaning.",
              image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT-HdPFE2H5Bwkbb3vQ2up8GvxZoL86lap4bg&s" },
            
            { title: "Viagens na Minha Terra", author: "Almeida Garrett", nationality: "pt", 
              details: "Uma mistura de romance e crônica sobre as viagens e a cultura portuguesa.", 
              details_en: "A mix of novel and chronicle about travels and Portuguese culture.",
              image: "https://m.media-amazon.com/images/I/91uO2Ddap6S._AC_UF1000,1000_QL80_.jpg" },
            
            { title: "O Velho da Horta / Auto da Barca do Inferno / A Farsa de Inês Pereira", author: "Gil Vicente", nationality: "pt", 
              details: "Três peças que representam a crítica social e o teatro português.", 
              details_en: "Three plays that represent social criticism and Portuguese theater.",
              image: "https://m.media-amazon.com/images/I/81Z4Ef5fR6L.jpg" }
        ];

        // Inicializa o carrossel
        function initCarousel() {
            const carouselInner = document.querySelector('.carousel-inner');
            const carouselIndicators = document.querySelector('.carousel-indicators');
            
            books.forEach((book, index) => {
                // Adiciona indicadores
                const indicator = document.createElement('button');
                indicator.type = 'button';
                indicator.dataset.bsTarget = '#bookCarousel';
                indicator.dataset.bsSlideTo = index;
                if (index === 0) indicator.classList.add('active');
                carouselIndicators.appendChild(indicator);
                
                // Adiciona itens do carrossel
                const carouselItem = document.createElement('div');
                carouselItem.classList.add('carousel-item');
                if (index === 0) carouselItem.classList.add('active');
                
                const img = document.createElement('img');
                img.src = book.image;
                img.alt = book.title;
                img.classList.add('d-block', 'w-100');
                
                const caption = document.createElement('div');
                caption.classList.add('carousel-caption', 'd-none', 'd-md-block');
                caption.innerHTML = `
                    <h5 class="book-title">${book.title}</h5>
                    <p class="book-author">${book.author}</p>
                `;
                
                carouselItem.appendChild(img);
                carouselItem.appendChild(caption);
                carouselInner.appendChild(carouselItem);
            });
        }

        // Exibe os livros na lista
        function displayBooks(filter = "") {
            const bookList = document.getElementById("books");
            bookList.innerHTML = "";
            
            const filteredBooks = books.filter(book => 
                book.title.toLowerCase().includes(filter.toLowerCase()) ||
                book.author.toLowerCase().includes(filter.toLowerCase())
            );
            
            if (filteredBooks.length === 0) {
                const noResults = document.createElement('div');
                noResults.classList.add('no-results');
                noResults.textContent = 'Nenhum livro encontrado. Tente outro termo de busca.';
                bookList.appendChild(noResults);
                return;
            }
            
            filteredBooks.forEach((book, index) => {
                const li = document.createElement("li");
                
                // Adiciona bandeira conforme a nacionalidade
                let flagSrc = "";
                if (book.nationality === "br") flagSrc = "https://flagcdn.com/w20/br.png";
                else if (book.nationality === "pt") flagSrc = "https://flagcdn.com/w20/pt.png";
                else if (book.nationality === "ru") flagSrc = "https://flagcdn.com/w20/ru.png";
                
                li.innerHTML = `
                    <span>${book.title} – ${book.author}</span>
                    ${flagSrc ? `<img src="${flagSrc}" class="flag-icon" alt="${book.nationality}">` : ''}
                `;
                
                li.addEventListener("click", () => toggleDetails(index));
                
                const detailsDiv = document.createElement("div");
                detailsDiv.classList.add("book-details");
                detailsDiv.innerHTML = `
                    <strong>Detalhes:</strong>
                    <p class="details-text">${book.details}</p>
                    <button class="translate-btn">Traduzir para Inglês</button>
                    <img src="${book.image}" alt="${book.title}" style="max-width: 200px; display: block; margin: 10px auto; border-radius: 5px;">
                `;
                
                // Adiciona evento de clique ao botão de tradução
                const translateBtn = detailsDiv.querySelector('.translate-btn');
                translateBtn.addEventListener('click', (e) => {
                    e.stopPropagation(); // Impede que o evento de clique no li seja acionado
                    const detailsText = detailsDiv.querySelector('.details-text');
                    if (translateBtn.textContent === 'Traduzir para Inglês') {
                        detailsText.textContent = book.details_en;
                        translateBtn.textContent = 'Ver em Português';
                    } else {
                        detailsText.textContent = book.details;
                        translateBtn.textContent = 'Traduzir para Inglês';
                    }
                });
                
                li.appendChild(detailsDiv);
                bookList.appendChild(li);
            });
        }

        function toggleDetails(index) {
            const bookList = document.getElementById("books");
            const bookItems = bookList.getElementsByTagName("li");
            const detailsDiv = bookItems[index].querySelector(".book-details");
            detailsDiv.style.display = detailsDiv.style.display === "block" ? "none" : "block";
        }

        // Inicialização
        document.addEventListener("DOMContentLoaded", () => {
            initCarousel();
            displayBooks();
            
            document.getElementById("search").addEventListener("input", function() {
                displayBooks(this.value);
            });
        });
    </script>
</body>
</html>
