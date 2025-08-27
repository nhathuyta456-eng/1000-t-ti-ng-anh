<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>1000 Common English Vocabulary Flashcards</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .flashcard {
            perspective: 1000px;
            transform-style: preserve-3d;
            transition: all 0.5s ease;
        }

        .card {
            transform-style: preserve-3d;
            transition: transform 0.6s ease;
        }

        .card.flipped {
            transform: rotateY(180deg);
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
        }

        .card-back {
            transform: rotateY(180deg);
        }

        .progress-bar {
            transition: width 0.3s ease;
        }

        .flip-button:hover {
            transform: scale(1.05);
            transition: transform 0.2s ease;
        }

        .category-badge {
            transition: all 0.3s ease;
        }

        .category-badge:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .fade-in {
            animation: fadeIn 0.5s ease-out;
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center py-8 px-4">
    <div class="w-full max-w-4xl mx-auto">
        <!-- Header -->
        <div class="text-center mb-8 fade-in">
            <h1 class="text-4xl md:text-5xl font-bold text-white mb-4 drop-shadow-lg">English Vocabulary Master</h1>
            <p class="text-xl text-white opacity-90 mb-6">1000 Most Common Words - Interactive Flashcards</p>
            
            <div class="bg-white bg-opacity-20 backdrop-blur-sm rounded-2xl p-6 mb-6">
                <div class="flex flex-wrap justify-center gap-4">
                    <div class="category-badge bg-blue-500 text-white px-4 py-2 rounded-full cursor-pointer hover:bg-blue-600">
                        All Words
                    </div>
                    <div class="category-badge bg-green-500 text-white px-4 py-2 rounded-full cursor-pointer hover:bg-green-600">
                        Nouns
                    </div>
                    <div class="category-badge bg-purple-500 text-white px-4 py-2 rounded-full cursor-pointer hover:bg-purple-600">
                        Verbs
                    </div>
                    <div class="category-badge bg-orange-500 text-white px-4 py-2 rounded-full cursor-pointer hover:bg-orange-600">
                        Adjectives
                    </div>
                </div>
            </div>
        </div>

        <!-- Progress Bar -->
        <div class="bg-white bg-opacity-20 backdrop-blur-sm rounded-xl p-4 mb-6">
            <div class="flex justify-between items-center mb-2">
                <span class="text-white font-semibold">Progress</span>
                <span class="text-white" id="progress-text">1/1000</span>
            </div>
            <div class="w-full bg-white bg-opacity-30 rounded-full h-3">
                <div class="progress-bar bg-gradient-to-r from-blue-400 to-purple-500 h-3 rounded-full" style="width: 0.1%"></div>
            </div>
        </div>

        <!-- Flashcard Container -->
        <div class="flashcard mb-8">
            <div class="card relative w-full h-96 md:h-80 cursor-pointer" id="main-card">
                <!-- Front of Card -->
                <div class="card-face front bg-white p-8 flex flex-col items-center justify-center">
                    <div class="text-4xl md:text-5xl font-bold text-gray-800 mb-4 text-center" id="word">Accept</div>
                    <div class="text-sm text-gray-500 uppercase tracking-wider" id="category">Verb</div>
                    <div class="absolute bottom-4 text-xs text-gray-400">
                        Click to see definition
                    </div>
                </div>
                
                <!-- Back of Card -->
                <div class="card-face back bg-gradient-to-br from-blue-100 to-purple-100 p-8 flex flex-col items-center justify-center">
                    <div class="text-2xl md:text-3xl font-bold text-gray-800 mb-2 text-center" id="word-back">Accept</div>
                    <div class="text-lg text-gray-600 mb-4 text-center" id="definition">to receive or take something offered</div>
                    <div class="text-sm text-gray-500 italic mb-2" id="example">"I accept your apology."</div>
                    <div class="text-xs text-gray-400 uppercase tracking-wider" id="pronunciation">/əkˈsept/</div>
                </div>
            </div>
        </div>

        <!-- Navigation Controls -->
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center">
            <button class="flip-button bg-white text-blue-600 px-6 py-3 rounded-full font-semibold hover:bg-blue-50 transition-all duration-200 flex items-center gap-2" id="flip-btn">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"></path>
                </svg>
                Flip Card
            </button>
            
            <div class="flex gap-4">
                <button class="flip-button bg-white text-gray-700 px-4 py-3 rounded-full font-semibold hover:bg-gray-100 transition-all duration-200" id="prev-btn" disabled>
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
                    </svg>
                </button>
                
                <button class="flip-button bg-blue-600 text-white px-4 py-3 rounded-full font-semibold hover:bg-blue-700 transition-all duration-200" id="next-btn">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
                    </svg>
                </button>
            </div>
            
            <button class="flip-button bg-green-500 text-white px-6 py-3 rounded-full font-semibold hover:bg-green-600 transition-all duration-200 flex items-center gap-2" id="mark-known">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                </svg>
                Mark as Known
            </button>
        </div>

        <!-- Stats Section -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-8">
            <div class="bg-white bg-opacity-20 backdrop-blur-sm rounded-xl p-4 text-center">
                <div class="text-2xl font-bold text-white" id="known-count">0</div>
                <div class="text-white opacity-80">Words Mastered</div>
            </div>
            <div class="bg-white bg-opacity-20 backdrop-blur-sm rounded-xl p-4 text-center">
                <div class="text-2xl font-bold text-white" id="remaining-count">1000</div>
                <div class="text-white opacity-80">Words to Learn</div>
            </div>
            <div class="bg-white bg-opacity-20 backdrop-blur-sm rounded-xl p-4 text-center">
                <div class="text-2xl font-bold text-white" id="completion">0%</div>
                <div class="text-white opacity-80">Complete</div>
            </div>
        </div>

        <!-- Learning Tips -->
        <div class="bg-white bg-opacity-20 backdrop-blur-sm rounded-xl p-6 mt-8">
            <h3 class="text-white text-lg font-semibold mb-3">Learning Tips</h3>
            <ul class="text-white opacity-90 space-y-2 text-sm">
                <li>• Study 10-20 words daily for best retention</li>
                <li>• Review previously learned words regularly</li>
                <li>• Use words in sentences to improve memory</li>
                <li>• Practice pronunciation with the phonetic guides</li>
            </ul>
        </div>

        <!-- Decorative Image -->
        <div class="mt-8 text-center">
            <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b6451379-10d7-42c2-850c-d476699c32f0.png" alt="Modern language learning setup with open books, laptop displaying vocabulary flashcards, and study materials on a wooden desk" class="rounded-2xl mx-auto shadow-xl">
        </div>
    </div>

    <script>
        // Sample vocabulary data (first 50 words as example)
        const vocabulary = [
            { word: "Accept", definition: "to receive or take something offered", category: "Verb", example: "I accept your apology.", pronunciation: "/əkˈsept/" },
            { word: "Achieve", definition: "to successfully complete something", category: "Verb", example: "She achieved her goals.", pronunciation: "/əˈtʃiːv/" },
            { word: "Across", definition: "from one side to the other", category: "Preposition", example: "Walk across the street.", pronunciation: "/əˈkrɒs/" },
            { word: "Act", definition: "to do something", category: "Verb", example: "Act now before it's too late.", pronunciation: "/ækt/" },
            { word: "Active", definition: "engaged in action", category: "Adjective", example: "He leads an active lifestyle.", pronunciation: "/ˈæktɪv/" },
            { word: "Actual", definition: "real or existing in fact", category: "Adjective", example: "The actual cost was higher.", pronunciation: "/ˈæktʃuəl/" },
            { word: "Add", definition: "to put something with another", category: "Verb", example: "Add sugar to the recipe.", pronunciation: "/æd/" },
            { word: "Address", definition: "the details of where someone lives", category: "Noun", example: "What's your address?", pronunciation: "/əˈdres/" },
            { word: "Adult", definition: "a fully grown person", category: "Noun", example: "Adults must take responsibility.", pronunciation: "/ˈædʌlt/" },
            { word: "Advantage", definition: "a beneficial factor", category: "Noun", example: "Height is an advantage in basketball.", pronunciation: "/ədˈvæntɪdʒ/" },
            { word: "Advertise", definition: "to promote a product", category: "Verb", example: "Companies advertise on television.", pronunciation: "/ˈædvətaɪz/" },
            { word: "Advice", definition: "guidance or recommendations", category: "Noun", example: "I need your advice.", pronunciation: "/ədˈvaɪs/" },
            { word: "Affect", definition: "to influence something", category: "Verb", example: "Weather affects our mood.", pronunciation: "/əˈfekt/" },
            { word: "Afford", definition: "to have enough money for", category: "Verb", example: "I can't afford a new car.", pronunciation: "/əˈfɔːd/" },
            { word: "Afraid", definition: "feeling fear", category: "Adjective", example: "I'm afraid of spiders.", pronunciation: "/əˈfreɪd/" },
            { word: "After", definition: "following in time", category: "Preposition", example: "We'll meet after lunch.", pronunciation: "/ˈɑːftə/" },
            { word: "Afternoon", definition: "the time between noon and evening", category: "Noun", example: "Good afternoon!", pronunciation: "/ˌɑːftəˈnuːn/" },
            { word: "Again", definition: "one more time", category: "Adverb", example: "Please say that again.", pronunciation: "/əˈɡen/" },
            { word: "Against", definition: "in opposition to", category: "Preposition", example: "I'm against that idea.", pronunciation: "/əˈɡenst/" },
            { word: "Age", definition: "how old someone is", category: "Noun", example: "What's your age?", pronunciation: "/eɪdʒ/" },
            { word: "Agency", definition: "a business providing services", category: "Noun", example: "Travel agency", pronunciation: "/ˈeɪdʒənsi/" },
            { word: "Agent", definition: "a person who acts for another", category: "Noun", example: "Real estate agent", pronunciation: "/ˈeɪdʒənt/" },
            { word: "Aggressive", definition: "ready to attack", category: "Adjective", example: "Aggressive behavior", pronunciation: "/əˈɡresɪv/" },
            { word: "Ago", definition: "before the present time", category: "Adverb", example: "Two years ago", pronunciation: "/əˈɡoʊ/" },
            { word: "Agree", definition: "to have the same opinion", category: "Verb", example: "I agree with you.", pronunciation: "/əˈɡriː/" },
            { word: "Ahead", definition: "in front", category: "Adverb", example: "Go ahead and start.", pronunciation: "/əˈhed/" },
            { word: "Aid", definition: "help or support", category: "Noun", example: "Foreign aid", pronunciation: "/eɪd/" },
            { word: "Aim", definition: "to point or direct", category: "Verb", example: "Aim carefully.", pronunciation: "/eɪm/" },
            { word: "Air", definition: "the invisible gas we breathe", category: "Noun", example: "Fresh air", pronunciation: "/eə/" },
            { word: "All", definition: "the whole amount", category: "Determiner", example: "All students", pronunciation: "/ɔːl/" },
            { word: "Allow", definition: "to give permission", category: "Verb", example: "Allow me to help.", pronunciation: "/əˈlaʊ/" },
            { word: "Almost", definition: "nearly", category: "Adverb", example: "Almost finished", pronunciation: "/ˈɔːlməʊst/" },
            { word: "Alone", definition: "without others", category: "Adjective", example: "She lives alone.", pronunciation: "/əˈləʊn/" },
            { word: "Along", definition: "moving in a constant direction", category: "Preposition", example: "Walk along the road.", pronunciation: "/əˈlɒŋ/" },
            { word: "Already", definition: "before now", category: "Adverb", example: "I already ate.", pronunciation: "/ɔːlˈredi/" },
            { word: "Also", definition: "in addition", category: "Adverb", example: "I also want coffee.", pronunciation: "/ˈɔːlsəʊ/" },
            { word: "Although", definition: "despite the fact that", category: "Conjunction", example: "Although it rained, we had fun.", pronunciation: "/ɔːlˈðəʊ/" },
            { word: "Always", definition: "at all times", category: "Adverb", example: "Always be kind.", pronunciation: "/ˈɔːlweɪz/" },
            { word: "Amazing", definition: "very surprising", category: "Adjective", example: "Amazing view!", pronunciation: "/əˈmeɪzɪŋ/" },
            { word: "Among", definition: "surrounded by", category: "Preposition", example: "Among friends", pronunciation: "/əˈmʌŋ/" },
            { word: "Amount", definition: "a quantity of something", category: "Noun", example: "Large amount", pronunciation: "/əˈmaʊnt/" },
            { word: "Analysis", definition: "detailed examination", category: "Noun", example: "Data analysis", pronunciation: "/əˈnæləsɪs/" },
            { word: "Ancient", definition: "very old", category: "Adjective", example: "Ancient civilization", pronunciation: "/ˈeɪnʃənt/" },
            { word: "And", definition: "used to connect words", category: "Conjunction", example: "Salt and pepper", pronunciation: "/ænd/" },
            { word: "Anger", definition: "strong feeling of annoyance", category: "Noun", example: "He felt great anger.", pronunciation: "/ˈæŋɡə/" },
            { word: "Angle", definition: "space between intersecting lines", category: "Noun", example: "Right angle", pronunciation: "/ˈæŋɡl/" },
            { word: "Angry", definition: "feeling anger", category: "Adjective", example: "Angry customer", pronunciation: "/ˈæŋɡri/" },
            { word: "Animal", definition: "living creature", category: "Noun", example: "Wild animal", pronunciation: "/ˈænɪməl/" },
            { word: "Announce", definition: "to make known publicly", category: "Verb", example: "Announce the winner.", pronunciation: "/əˈnaʊns/" },
            { word: "Annual", definition: "occurring once a year", category: "Adjective", example: "Annual meeting", pronunciation: "/ˈænjuəl/" }
        ];

        let currentIndex = 0;
        let knownWords = new Set();

        // DOM Elements
        const cardElement = document.getElementById('main-card');
        const flipBtn = document.getElementById('flip-btn');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const markKnownBtn = document.getElementById('mark-known');
        const progressText = document.getElementById('progress-text');
        const progressBar = document.querySelector('.progress-bar');
        const knownCount = document.getElementById('known-count');
        const remainingCount = document.getElementById('remaining-count');
        const completion = document.getElementById('completion');

        // Initialize the first card
        updateCard();

        // Event Listeners
        cardElement.addEventListener('click', flipCard);
        flipBtn.addEventListener('click', flipCard);
        prevBtn.addEventListener('click', showPreviousCard);
        nextBtn.addEventListener('click', showNextCard);
        markKnownBtn.addEventListener('click', markAsKnown);

        function updateCard() {
            const currentWord = vocabulary[currentIndex];
            
            // Update front of card
            document.getElementById('word').textContent = currentWord.word;
            document.getElementById('category').textContent = currentWord.category;
            
            // Update back of card
            document.getElementById('word-back').textContent = currentWord.word;
            document.getElementById('definition').textContent = currentWord.definition;
            document.getElementById('example').textContent = currentWord.example;
            document.getElementById('pronunciation').textContent = currentWord.pronunciation;
            
            // Update progress
            progressText.textContent = `${currentIndex + 1}/1000`;
            progressBar.style.width = `${((currentIndex + 1) / 1000) * 100}%`;
            
            // Update navigation buttons
            prevBtn.disabled = currentIndex === 0;
            nextBtn.disabled = currentIndex === vocabulary.length - 1;
            
            // Update stats
            updateStats();
            
            // Reset card to front
            cardElement.classList.remove('flipped');
        }

        function flipCard() {
            cardElement.classList.toggle('flipped');
        }

        function showPreviousCard() {
            if (currentIndex > 0) {
                currentIndex--;
                updateCard();
            }
        }

        function showNextCard() {
            if (currentIndex < vocabulary.length - 1) {
                currentIndex++;
                updateCard();
            }
        }

        function markAsKnown() {
            const currentWord = vocabulary[currentIndex].word;
            if (knownWords.has(currentWord)) {
                knownWords.delete(currentWord);
                markKnownBtn.innerHTML = '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg> Mark as Known';
                markKnownBtn.classList.remove('bg-gray-500');
                markKnownBtn.classList.add('bg-green-500', 'hover:bg-green-600');
            } else {
                knownWords.add(currentWord);
                markKnownBtn.innerHTML = '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg> Mark as Unknown';
                markKnownBtn.classList.remove('bg-green-500', 'hover:bg-green-600');
                markKnownBtn.classList.add('bg-gray-500', 'hover:bg-gray-600');
            }
            updateStats();
        }

        function updateStats() {
            knownCount.textContent = knownWords.size;
            remainingCount.textContent = 1000 - knownWords.size;
            const completionPercentage = Math.round((knownWords.size / 1000) * 100);
            completion.textContent = `${completionPercentage}%`;
        }

        // Add keyboard navigation
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') showPreviousCard();
            if (e.key === 'ArrowRight') showNextCard();
            if (e.key === ' ') flipCard();
            if (e.key === 'Enter') markAsKnown();
        });

        // Smooth animations
        document.querySelectorAll('.category-badge').forEach(badge => {
            badge.addEventListener('click', () => {
                alert('Category filtering feature coming soon!');
            });
        });
    </script>
</body>
</html>

