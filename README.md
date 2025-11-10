<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Georgia's New South — Interactive Profiles (8th Grade)</title>
  <style>
    :root {
      --ink: #1f2937; --muted:#6b7280; --card:#ffffff; --bg:#f5f7fa; --accent:#2563eb; --good:#10b981; --bad:#ef4444;
    }
    *{box-sizing:border-box}
    body{font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;background:var(--bg);margin:0;color:var(--ink)}
    header{background:#1d4ed8;color:#fff;padding:22px 16px;text-align:center}
    header h1{margin:0 0 6px}
    .objective,.progress,.grid{max-width:1000px;margin:16px auto;padding:0 12px}
    .objective-inner{background:#fff;border:1px solid #e5e7eb;border-radius:12px;padding:14px}
    .grid{display:grid;grid-template-columns:repeat(12,1fr);gap:14px}
    .card{grid-column:span 12;background:var(--card);border:1px solid #e5e7eb;border-radius:14px;box-shadow:0 4px 14px rgba(0,0,0,.06);overflow:hidden}
    @media(min-width:860px){.card{display:grid;grid-template-columns:300px 1fr}}
    .media img{display:block;width:100%;height:100%;object-fit:cover}
    .body{padding:14px 16px}
    .tag{display:inline-block;background:#e0e7ff;color:#3730a3;padding:3px 10px;border-radius:999px;font-size:.8rem;font-weight:700}
    .title{margin:6px 0 6px}
    .bio,.connect{color:var(--muted);line-height:1.6}
    .links{margin-top:8px;display:flex;gap:8px;flex-wrap:wrap}
    .links a{display:inline-block;background:var(--accent);color:#fff;text-decoration:none;padding:8px 12px;border-radius:8px;border:1px solid #1e40af}
    .links a.secondary{background:#fff;color:#1f2937;border-color:#d1d5db}
    .quiz{margin-top:12px;border-top:1px dashed #e5e7eb;padding-top:10px}
    .choice{display:block;margin:6px 0;padding:8px 10px;border-radius:10px;border:1px solid #e5e7eb;background:#fff;cursor:pointer}
    .choice.correct{background:#ecfdf5;border-color:#a7f3d0}
    .choice.incorrect{background:#fef2f2;border-color:#fecaca}
    .progress .wrap{background:#fff;border:1px solid #e5e7eb;border-radius:999px;padding:6px 10px;display:flex;align-items:center;gap:10px}
    .bar{flex:1;height:10px;border-radius:999px;background:#e5e7eb;overflow:hidden}
    #barFill{display:block;height:10px;width:0%}
    .score{font-size:.9rem;color:var(--muted)}
    .btn{background:var(--accent);color:#fff;border:0;border-radius:10px;padding:8px 12px;cursor:pointer}
  </style>
</head>
<body>
  <header>
    <h1>Georgia's New South — Interactive Profiles</h1>
    <p>Grade 8 • Explore key figures and evaluate the political, social, and economic changes of the New South Era.</p>
  </header>

  <section class="objective">
    <div class="objective-inner">
      <strong>Objective:</strong> Evaluate key political, social, and economic changes that occurred in Georgia during the New South Era. Use the profiles below to learn, watch a short video, and answer quick-check questions.
    </div>
  </section>

  <main class="grid" id="cards"></main>

  <!-- Teacher note: To guarantee images load on school networks, upload an **img/** folder alongside this HTML
       (DriveToWeb or your host) with these filenames:
       - img/bourbon-triumvirate.jpg
       - img/henry-grady.jpg
       - img/tom-watson.jpg
       - img/booker-t-washington.jpg
       - img/web-du-bois.jpg
       - img/alonzo-herndon.jpg
       - img/john-lugenia-hope.jpg
       If a local file is missing, the app will try a safe remote image. If that also fails, it shows a clean SVG placeholder. -->

  <section class="progress">
    <div class="wrap">
      <div class="bar"><span id="barFill"></span></div>
      <div class="score" id="scoreText">0 correct</div>
      <button class="btn" id="restartBtn">Restart</button>
    </div>
  </section>

  <script>
    const teacherPrompts = {
      bourbon: 'https://georgiastudies.gpb.org/c15-s1#Bourbon-Redeemers',
      grady: 'https://georgiastudies.gpb.org/c15-s3#Today-in-Georgia-History:-Henry-Grady',
      watson: 'https://georgiastudies.gpb.org/c15-s1#Tom-Watson',
      btw: 'https://www.ducksters.com/biography/booker_t_washington.php',
      dubois: 'https://kids.britannica.com/kids/article/WEB-Du-Bois/353068',
      herndon: 'https://www.georgiaencyclopedia.org/articles/business-economy/alonzo-herndon-1858-1927/',
      hope: 'https://www.georgiaencyclopedia.org/articles/education/john-and-lugenia-burns-hope/'
    };

    const people = [
      // Tip: add a local image into an `img/` folder (DriveToWeb or your host) with these exact filenames.
      // The app will try the local image first, then the remote Wikimedia URL, then a built-in SVG.

      {
        id: 'bourbon',
        name: 'Bourbon Triumvirate',
        years: '1870s–1890s',
        // Local first (works best when hosted on Google/DriveToWeb)
        localImage: 'img/bourbon-triumvirate.jpg',
        // Remote fallback
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/John_B._Gordon_-_Brady-Handy.jpg/640px-John_B._Gordon_-_Brady-Handy.jpg',
        imageCaption: 'Joseph E. Brown • Alfred H. Colquitt • John B. Gordon',
        tag: 'Politics & Economy',
        bio: `The Bourbon Triumvirate—Joseph E. Brown, Alfred H. Colquitt, and John B. Gordon—dominated Georgia politics after Reconstruction. They promoted low taxes, reduced government spending, and closer ties with Northern industry. Their leadership favored railroads and big business, often at the expense of poor farmers and African Americans.`,
        connection: `They pushed a “New South” focused on industrial growth (textiles, railroads) and reconciliation with the North, while supporting policies—like disenfranchisement—that limited political power for many.`,
        video: 'https://www.youtube.com/results?search_query=bourbon+triumvirate+georgia',
        questions: [
          { q: 'What was a major economic goal of the Bourbon Triumvirate?', choices: ['Expanding plantations and slavery', 'Industrial growth and business investment', 'Full voting rights for all citizens', 'Isolation from Northern trade'], answer: 1 },
          { q: 'Which statement best describes their impact on democracy in Georgia?', choices: ['They expanded voting rights widely.', 'They limited the influence of railroads.', 'They supported policies that restricted many voters.', 'They refused to work with Northern businesses.'], answer: 2 }
        ]
      },
      {
        id: 'grady',
        name: 'Henry Grady',
        years: '1850–1889',
        localImage: 'img/henry-grady.jpg',
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Henry_W_Grady_1887.jpg/640px-Henry_W_Grady_1887.jpg',
        imageCaption: 'Editor of the Atlanta Constitution',
        tag: 'Media & Growth',
        bio: `As editor of the Atlanta Constitution, Henry Grady became the leading spokesperson for the “New South.” He promoted Atlanta as a modern city built on factories, railroads, and trade—not just farming. Grady hosted industrial expositions to attract investors to Georgia.`,
        connection: `Grady’s boosterism helped shift Georgia’s economy toward industry and urbanization, although his vision often ignored the realities of segregation and inequality.`,
        video: 'https://youtu.be/oNeC7i5K5lE?si=fk9o5etPHeMxvFR_',
        questions: [
          { q: 'Henry Grady encouraged the South to focus on…', choices: ['Plantation agriculture only', 'Industrialization and urban growth', 'Avoiding national markets', 'Returning to Reconstruction policies'], answer: 1 },
          { q: 'How did Grady try to attract investment?', choices: ['By closing railroads', 'By organizing industrial expositions', 'By banning factories', 'By raising state taxes a lot'], answer: 1 }
        ]
      },
      {
        id: 'watson',
        name: 'Tom Watson & the Populists',
        years: '1856–1922 (Watson)',
        localImage: 'img/tom-watson.jpg',
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/97/Thomas_Edward_Watson_1915.jpg/640px-Thomas_Edward_Watson_1915.jpg',
        imageCaption: 'Leader in the Populist movement',
        tag: 'Populism & Reform',
        bio: `Tom Watson spoke for struggling farmers in the 1890s. Early in his career, he supported the Farmers’ Alliance and rural free delivery (RFD) of mail. He criticized railroads and big businesses for unfair rates. Later in life, however, he turned toward nativist and white supremacist positions.`,
        connection: `The Populists demanded fairer railroad rates, easier credit, and political reforms—spotlighting the New South’s deep rural economic problems.`,
        video: 'https://youtu.be/WljCQsOSKdc?si=lQQb6OvHy8MVU2Nu',
        questions: [
          { q: 'Which reform is closely associated with Tom Watson’s early work?', choices: ['Rural Free Delivery (RFD) of mail', 'Outlawing railroads', 'Ending public schools', 'Building only cotton mills'], answer: 0 },
          { q: 'Populists mainly represented the interests of…', choices: ['Urban bankers', 'Small farmers and laborers', 'Northern factory owners', 'Only newspaper editors'], answer: 1 }
        ]
      },
      {
        id: 'btw',
        name: 'Booker T. Washington',
        years: '1856–1915',
        localImage: 'img/booker-t-washington.jpg',
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/BookerTWashingtonRetouched.jpg/640px-BookerTWashingtonRetouched.jpg',
        imageCaption: 'Educator; leader at Tuskegee Institute',
        tag: 'Education & Economy',
        bio: `Booker T. Washington founded Tuskegee Institute and advocated vocational education. In his 1895 “Atlanta Compromise” speech, he suggested that African Americans focus on job skills and economic progress first, while avoiding direct challenges to segregation—an approach widely debated then and now.`,
        connection: `His ideas aligned with parts of the New South’s emphasis on industry and skilled labor, yet they also accepted a segregated social order.`,
        video: 'https://youtu.be/07cispyOhWQ?si=gR1WscYEGNrV9l8X',
        questions: [
          { q: 'What did Washington emphasize in the 1895 Atlanta speech?', choices: ['Immediate full social equality', 'Vocational training and economic progress', 'Closing all factories', 'Ending public education'], answer: 1 },
          { q: 'Washington’s approach was often criticized for…', choices: ['Encouraging violence', 'Rejecting any schooling', 'Accommodating segregation', 'Opposing any work skills'], answer: 2 }
        ]
      },
      {
        id: 'dubois',
        name: 'W. E. B. Du Bois',
        years: '1868–1963',
        localImage: 'img/web-du-bois.jpg',
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/WEB_DuBois_1918.jpg/640px-WEB_DuBois_1918.jpg',
        imageCaption: 'Scholar at Atlanta University; NAACP co-founder',
        tag: 'Civil Rights & Scholarship',
        bio: `A scholar and activist who taught at Atlanta University, W. E. B. Du Bois argued for immediate civil rights and higher education for the “Talented Tenth.” He helped found the NAACP in 1909 and challenged segregation through research, writing, and legal strategies.`,
        connection: `Du Bois offered a competing vision to Washington’s—insisting the New South must include political equality and access to advanced education.`,
        video: 'https://youtu.be/wemGETdjx0w?si=pqyJVAIrO0WaPh7P',
        questions: [
          { q: 'Du Bois believed progress required…', choices: ['Only vocational training', 'Immediate civil rights and higher education', 'Ending all colleges', 'Isolation from national politics'], answer: 1 },
          { q: 'Which organization did Du Bois help found?', choices: ['The NAACP', 'The AAA', 'The FDA', 'The CCC'], answer: 0 }
        ]
      },
      {
        id: 'herndon',
        name: 'Alonzo Herndon',
        years: '1858–1927',
        localImage: 'img/alonzo-herndon.jpg',
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Alonzo_F._Herndon.jpg/640px-Alonzo_F._Herndon.jpg',
        imageCaption: 'Entrepreneur; Atlanta Life Insurance Company',
        tag: 'Entrepreneurship',
        bio: `Born into slavery, Alonzo Herndon became one of Atlanta’s wealthiest Black entrepreneurs. Starting with a barbershop business, he later founded the Atlanta Life Insurance Company, which offered policies to Black customers often excluded elsewhere.`,
        connection: `Herndon’s success highlights opportunities in the New South’s growing urban economy—while also revealing how segregation shaped where and for whom services were available.`,
        video: 'https://youtu.be/l4jZGA-Vdt4?si=WEEQXYDsaO9_MOBb',
        questions: [
          { q: 'What industry made Herndon most famous?', choices: ['Railroad construction', 'Insurance and business ownership', 'Newspaper editing', 'Cotton farming only'], answer: 1 },
          { q: 'Herndon’s company mainly served…', choices: ['Customers excluded by segregation', 'Only Northern investors', 'Only plantation owners', 'Only politicians'], answer: 0 }
        ]
      },
      {
        id: 'hope',
        name: 'John and Lugenia D. Burns Hope',
        years: '1871–1950 (John) & 1871–1947 (Lugenia)',
        localImage: 'img/john-lugenia-hope.jpg',
        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/JHope.jpg/640px-JHope.jpg',
        imageCaption: 'Leaders in education and social reform',
        tag: 'Education & Civil Rights',
        bio: `John Hope was the first Black president of Morehouse College and later Atlanta University. His wife, Lugenia Burns Hope, founded the Neighborhood Union, one of the first social service organizations for African Americans in Atlanta. Together, they worked for racial equality, education, and community improvement.`,
        connection: `The Hopes symbolized the progressive activism of African Americans in the New South—focusing on education, civic organization, and civil rights for Black communities.`,
        video: 'https://youtu.be/9cu-RhZf-2U?si=fYhSKMXTPPO-gijz&t=402',
        questions: [
          { q: 'What organization did Lugenia Burns Hope establish to help African Americans in Atlanta?', choices: ['The Neighborhood Union', 'NAACP', 'Tuskegee Institute', 'Atlanta Life Insurance Company'], answer: 0 },
          { q: 'John Hope was the first Black president of which institution?', choices: ['Spelman College', 'Morehouse College', 'Atlanta Constitution', 'Georgia Tech'], answer: 1 }
        ]
      }
    ];

    const cardsEl = document.getElementById('cards');
    const restartBtn = document.getElementById('restartBtn');
    const scoreText = document.getElementById('scoreText');
    const barFill = document.getElementById('barFill');

    const totalQuestions = people.reduce((sum, p) => sum + p.questions.length, 0);
    let correctCount = 0;
    const answered = new Map();

    function renderCards(){
      cardsEl.innerHTML = '';
      people.forEach(person => {
        const card = document.createElement('article');
        card.className = 'card';

        const media = document.createElement('div');
        media.className = 'media';
        const img = document.createElement('img');
        img.alt = person.name;
        const sources = [person.localImage, person.image];
        let srcIdx = 0;
        function tryNext(){
          if (srcIdx < sources.length){
            img.src = sources[srcIdx++];
          } else {
            const svg = `<svg xmlns='http://www.w3.org/2000/svg' width='640' height='480'>
              <rect width='100%' height='100%' fill='#e5e7eb'/>
              <text x='50%' y='50%' dominant-baseline='middle' text-anchor='middle' font-family='Arial' font-size='28' fill='#374151'>${person.name}</text>
            </svg>`;
            img.src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svg);
          }
        }
        img.referrerPolicy = 'no-referrer';
        img.onerror = tryNext;
        tryNext();
        media.appendChild(img);

        const body = document.createElement('div');
        body.className = 'body';
        body.innerHTML = `
          <span class="tag">${person.tag}</span>
          <h2 class="title">${person.name} <span style="font-size:.85rem;color:var(--muted);font-weight:600">${person.years||''}</span></h2>
          <p class="bio">${person.bio}</p>
          <p class="connect"><strong>Connection to the New South:</strong> ${person.connection}</p>
        `;

        const links = document.createElement('div');
        links.className = 'links';
        const videoA = document.createElement('a');
        videoA.href = person.video; videoA.target = '_blank'; videoA.rel = 'noopener'; videoA.textContent = 'Watch: Intro Video';
        const promptA = document.createElement('a');
        promptA.href = teacherPrompts[person.id] || '#'; promptA.target = '_blank'; promptA.rel = 'noopener'; promptA.textContent = 'Teacher Prompt'; promptA.className = 'secondary';
        links.appendChild(videoA); links.appendChild(promptA);
        body.appendChild(links);

        const quiz = document.createElement('div');
        quiz.className = 'quiz';
        person.questions.forEach((qset, idx) => {
          const q = document.createElement('p'); q.style.fontWeight = '700'; q.textContent = qset.q; quiz.appendChild(q);
          qset.choices.forEach((choice, cIdx) => {
            const btn = document.createElement('button');
            btn.className = 'choice'; btn.textContent = choice;
            btn.addEventListener('click', () => handleAnswer(`${person.id}-${idx}`, cIdx, qset.answer, btn, quiz));
            quiz.appendChild(btn);
          });
        });
        body.appendChild(quiz);

        card.appendChild(media); card.appendChild(body);
        cardsEl.appendChild(card);
      });
    }

    function handleAnswer(key, selectedIdx, correctIdx, btn, quizRoot){
      if (answered.has(key)) return;
      const isCorrect = selectedIdx === correctIdx;
      answered.set(key, isCorrect);
      if (isCorrect) btn.classList.add('correct'); else btn.classList.add('incorrect');
      correctCount += isCorrect ? 1 : 0;
      const buttons = Array.from(quizRoot.querySelectorAll('.choice')).slice(-4);
      buttons.forEach(b => b.disabled = true);
      updateProgress();
    }

    function updateProgress(){
      const pct = Math.round((correctCount / totalQuestions) * 100);
      barFill.style.width = pct + '%';
      barFill.style.background = `linear-gradient(90deg, #2563eb, #7c3aed ${pct}%)`;
      scoreText.textContent = `${correctCount} of ${totalQuestions} correct`;
    }

    restartBtn.addEventListener('click', () => {
      correctCount = 0; answered.clear(); renderCards(); updateProgress();
      window.scrollTo({ top: 0, behavior: 'smooth' });
    });

    renderCards();
    updateProgress();
  </script>
</body>
</html>
