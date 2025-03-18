
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>AI Resume Builder | Modern CV Creator</title>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet" />
  <!-- Font Awesome for Social Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
  <!-- jsPDF and html2canvas -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    /* Global Styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }
    body {
      background: #0B0C10;
      color: #C5C6C7;
      line-height: 1.6;
    }

    /* Header */
    .header {
      background: #1F2833;
      padding: 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      animation: fadeInDown 1s;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    .logo {
      display: flex;
      align-items: center;
    }
    .logo-circle {
      width: 50px;
      height: 50px;
      background: linear-gradient(135deg, #66FCF1, #45A29E);
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      margin-right: 1rem;
    }
    .logo-circle span {
      font-size: 1.5rem;
      font-weight: bold;
      color: #1F2833;
    }
    .header h1 {
      color: #66FCF1;
      font-size: 2rem;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    }

    /* Navigation */
    .toolbar {
      display: flex;
      align-items: center;
      gap: 1rem;
    }
    .nav-links {
      display: flex;
      gap: 1.5rem;
      list-style: none;
    }
    .nav-links a {
      color: #C5C6C7;
      text-decoration: none;
      padding: 0.5rem 1rem;
      border-radius: 25px;
      transition: all 0.3s ease;
    }
    .nav-links a:hover {
      background: #66FCF1;
      color: #1F2833;
      transform: translateY(-2px);
    }

    /* Main Container */
    .container {
      max-width: 1200px;
      margin: 2rem auto;
      padding: 0 1rem;
      display: flex;
      gap: 30px;
    }

    /* Card Styles */
    .card {
      background: #1F2833;
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      margin-bottom: 2rem;
    }
    .input-section, .preview-section {
      flex: 1;
    }
    .form-group {
      margin-bottom: 20px;
    }
    label {
      display: block;
      margin-bottom: 8px;
      color: #C5C6C7;
      font-weight: 500;
    }
    input, textarea, select {
      width: 100%;
      padding: 12px;
      border: 1px solid #66FCF1;
      border-radius: 8px;
      font-size: 14px;
      background: #0B0C10;
      color: #C5C6C7;
      transition: border-color 0.3s;
    }
    input:focus, textarea:focus, select:focus {
      outline: none;
      border-color: #45A29E;
    }

    /* Buttons */
    .download-btn, .clear-btn, .add-section-btn {
      border: 2px solid;
      padding: 12px 30px;
      font-size: 16px;
      cursor: pointer;
      border-radius: 25px;
      transition: all 0.3s ease;
      background: transparent;
      outline: none;
    }
    .download-btn {
      border-color: #66FCF1;
      color: #66FCF1;
      margin-top: 20px;
    }
    .download-btn:hover {
      background: #66FCF1;
      color: #1F2833;
      transform: translateY(-2px);
    }
    .clear-btn {
      border-color: #ff4757;
      color: #ff4757;
      margin-left: 10px;
      margin-top: 20px;
    }
    .clear-btn:hover {
      background: #ff4757;
      color: #1F2833;
      transform: translateY(-2px);
    }
    .add-section-btn {
      border-color: #4CAF50;
      color: #4CAF50;
      margin-top: 10px;
    }
    .add-section-btn:hover {
      background: #4CAF50;
      color: #1F2833;
      transform: translateY(-2px);
    }
    .download-btn:active, .clear-btn:active, .add-section-btn:active {
      transform: scale(0.95);
    }

    /* Dynamic Section */
    .dynamic-section {
      margin-bottom: 20px;
    }
    .dynamic-section textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #66FCF1;
      border-radius: 8px;
      font-size: 14px;
      background: #0B0C10;
      color: #C5C6C7;
    }

    /* Gorgeous Resume Template */
    .resume-preview {
      display: flex;
      flex-direction: row;
      border-radius: 15px;
      overflow: hidden;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
      background: #1F2833;
    }
    .resume-sidebar {
      width: 35%;
      background: linear-gradient(180deg, #1F2833 0%, #0B0C10 100%);
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      border-right: 2px solid #66FCF1;
    }
    .resume-sidebar .profile-img {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      object-fit: cover;
      border: 3px solid #66FCF1;
      margin-bottom: 15px;
    }
    .resume-sidebar h1 {
      color: #66FCF1;
      font-size: 1.8rem;
      margin-bottom: 5px;
      text-align: center;
    }
    .resume-sidebar p {
      font-size: 0.9rem;
      text-align: center;
      margin-bottom: 5px;
    }
    .resume-sidebar a {
      color: #66FCF1;
      text-decoration: none;
      font-size: 0.9rem;
    }
    .resume-sidebar .skills-section {
      width: 100%;
      margin-top: 20px;
    }
    .resume-sidebar .skills-section .section-title {
      text-align: center;
      margin-bottom: 10px;
      font-size: 1rem;
    }
    .resume-sidebar .skill-tags {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }
    .resume-sidebar .skill-tag {
      background: #66FCF1;
      color: #1F2833;
      padding: 5px 10px;
      border-radius: 20px;
      font-size: 0.8rem;
    }
    .resume-main {
      width: 65%;
      padding: 20px;
    }
    .resume-main .resume-section {
      margin-bottom: 20px;
    }
    .resume-main .section-title {
      color: #66FCF1;
      font-size: 1.2rem;
      border-bottom: 2px solid #66FCF1;
      padding-bottom: 5px;
      margin-bottom: 10px;
    }
    .resume-main p {
      font-size: 0.95rem;
      line-height: 1.4;
    }
    /* Dynamic Sections appear in the main area */
    #dynamicSections {
      margin-top: 20px;
    }

    /* Footer */
    .footer {
      background: #1F2833;
      padding: 2rem 1rem;
      margin-top: 2rem;
      text-align: center;
      color: #C5C6C7;
      border-top: 2px solid #66FCF1;
      box-shadow: 0 -4px 6px rgba(0, 0, 0, 0.1);
    }
    .footer-links {
      display: flex;
      justify-content: center;
      gap: 1.5rem;
      margin-bottom: 1rem;
    }
    .footer-links a {
      color: #C5C6C7;
      text-decoration: none;
      transition: all 0.3s ease;
    }
    .footer-links a:hover {
      color: #66FCF1;
      transform: translateY(-2px);
    }
    .social-icons {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-top: 1rem;
    }
    .social-icons a {
      color: #C5C6C7;
      font-size: 1.5rem;
      transition: all 0.3s ease;
    }
    .social-icons a:hover {
      color: #66FCF1;
      transform: translateY(-2px);
    }

    @keyframes fadeInDown {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Responsive */
    @media (max-width: 768px) {
      .header { flex-direction: column; align-items: flex-start; }
      .toolbar { flex-direction: column; align-items: flex-start; width: 100%; margin-top: 1rem; }
      .nav-links { flex-direction: column; gap: 1rem; width: 100%; }
      .nav-links a { width: 100%; text-align: center; }
      .container { flex-direction: column; }
      .resume-preview { flex-direction: column; }
      .resume-sidebar, .resume-main { width: 100%; }
      .resume-sidebar { border-right: none; border-bottom: 2px solid #66FCF1; }
    }
  </style>
</head>
<body>
  <!-- Header -->
  <header class="header">
    <div class="logo">
      <div class="logo-circle">
        <span>MN</span>
      </div>
      <h1>Masud Neill AI Resume Builder</h1>
    </div>
    <div class="toolbar">
      <ul class="nav-links">
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#services">Services</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
  </header>

  <!-- Main Content -->
  <div class="container">
    <!-- Input Section -->
    <div class="input-section">
      <div class="card">
        <h2>Resume Details</h2>
        <div class="form-group">
          <label>Full Name</label>
          <input type="text" id="name" placeholder="Enter your full name" required>
        </div>
        <div class="form-group">
          <label>Profile Photo</label>
          <input type="file" id="photo" accept="image/*" required>
        </div>
        <div class="form-group">
          <label>Email Address</label>
          <input type="email" id="email" placeholder="Enter your email" required>
        </div>
        <div class="form-group">
          <label>Phone Number</label>
          <input type="tel" id="phone" placeholder="Enter your phone number" required>
        </div>
        <div class="form-group">
          <label>LinkedIn Profile</label>
          <input type="url" id="linkedin" placeholder="Enter your LinkedIn profile URL">
        </div>
        <div class="form-group">
          <label>GitHub Profile</label>
          <input type="url" id="github" placeholder="Enter your GitHub profile URL">
        </div>
        <div class="form-group">
          <label>Objective</label>
          <textarea id="objective" rows="3" placeholder="Write a short objective statement"></textarea>
        </div>
        <div class="form-group">
          <label>Education Level</label>
          <input type="text" id="education" placeholder="e.g. Bachelor of Computer Science" required>
        </div>
        <div class="form-group">
          <label>Skills (comma separated)</label>
          <input type="text" id="skills" placeholder="e.g. Web Development, Graphic Design" required>
        </div>
        <div class="form-group">
          <label>Experience</label>
          <textarea id="experience" rows="4" placeholder="Describe your work experience" required></textarea>
        </div>
        <button class="add-section-btn" onclick="addSection('Projects')">Add Projects</button>
        <button class="add-section-btn" onclick="addSection('Certifications')">Add Certifications</button>
        <button class="add-section-btn" onclick="addSection('Languages')">Add Languages</button>
      </div>
    </div>

    <!-- Preview Section -->
    <div class="preview-section">
      <div class="card">
        <h2>Resume Preview</h2>
        <div class="resume-preview" id="resumePreview">
          <div class="resume-sidebar">
            <img src="" alt="Profile Photo" class="profile-img" id="previewPhoto">
            <h1 id="previewName">John Doe</h1>
            <p id="previewContact">john@email.com</p>
            <p id="previewLinks"></p>
            <div class="skills-section">
              <h3 class="section-title">Skills</h3>
              <div class="skill-tags" id="previewSkills">
                <span class="skill-tag">Web Development</span>
                <span class="skill-tag">Graphic Design</span>
              </div>
            </div>
          </div>
          <div class="resume-main">
            <div class="resume-section">
              <h3 class="section-title">Objective</h3>
              <p id="previewObjective">To leverage my skills in web development and design to create impactful solutions.</p>
            </div>
            <div class="resume-section">
              <h3 class="section-title">Education</h3>
              <p id="previewEducation">Bachelor of Computer Science - University Name</p>
            </div>
            <div class="resume-section">
              <h3 class="section-title">Experience</h3>
              <div id="previewExperience">
                <div class="experience-item">
                  <p>• Senior Developer at XYZ Company (2020-Present)</p>
                  <p>• Developed multiple web applications</p>
                </div>
              </div>
            </div>
            <div id="dynamicSections"></div>
          </div>
        </div>
        <button class="download-btn" onclick="downloadPDF()">Download Resume</button>
        <button class="clear-btn" onclick="clearResume()">Clear Resume</button>
      </div>
    </div>
  </div>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-links">
      <a href="#home">Home</a>
      <a href="#about">About</a>
      <a href="#services">Services</a>
      <a href="#contact">Contact</a>
    </div>
    <div class="social-icons">
      <a href="https://facebook.com" target="_blank"><i class="fab fa-facebook-f"></i></a>
      <a href="https://twitter.com" target="_blank"><i class="fab fa-twitter"></i></a>
      <a href="https://linkedin.com" target="_blank"><i class="fab fa-linkedin-in"></i></a>
      <a href="https://instagram.com" target="_blank"><i class="fab fa-instagram"></i></a>
    </div>
    <p>© 2025 Masud Neill. All rights reserved.</p>
  </footer>

  <script>
    // Real-time Preview Update
    document.querySelectorAll('input, textarea, select').forEach(element => {
      element.addEventListener('input', updatePreview);
    });

    document.getElementById('photo').addEventListener('change', function(e) {
      const reader = new FileReader();
      reader.onload = function() {
        document.getElementById('previewPhoto').src = reader.result;
      }
      reader.readAsDataURL(e.target.files[0]);
    });

    function updatePreview() {
      document.getElementById('previewName').textContent = document.getElementById('name').value;
      document.getElementById('previewContact').textContent =
        `${document.getElementById('email').value} | ${document.getElementById('phone').value}`;
      document.getElementById('previewLinks').innerHTML =
        `<a href="${document.getElementById('linkedin').value}" target="_blank">LinkedIn</a> | 
         <a href="${document.getElementById('github').value}" target="_blank">GitHub</a>`;
      document.getElementById('previewObjective').textContent = document.getElementById('objective').value;
      document.getElementById('previewEducation').textContent = document.getElementById('education').value;
      
      // Update Skills
      const skills = document.getElementById('skills').value.split(',').map(skill => skill.trim());
      const skillsContainer = document.getElementById('previewSkills');
      skillsContainer.innerHTML = skills.filter(skill => skill).map(skill =>
        `<span class="skill-tag">${skill}</span>`
      ).join('');
      
      // Update Experience
      const experiencePoints = document.getElementById('experience').value.split('\n').filter(point => point.trim() !== '');
      const experienceContainer = document.getElementById('previewExperience');
      experienceContainer.innerHTML = experiencePoints.map(point =>
        `<div class="experience-item"><p>• ${point}</p></div>`
      ).join('');
    }

    // Add Dynamic Sections
    function addSection(sectionName) {
      const inputSection = document.querySelector('.input-section .card');
      const previewSection = document.getElementById('dynamicSections');

      // Add input field
      const inputHTML = `
        <div class="dynamic-section">
          <label>${sectionName}</label>
          <textarea id="${sectionName.toLowerCase()}" rows="3" placeholder="Add ${sectionName.toLowerCase()}"></textarea>
        </div>
      `;
      inputSection.insertAdjacentHTML('beforeend', inputHTML);

      // Add preview section
      const previewHTML = `
        <div class="resume-section">
          <h3 class="section-title">${sectionName}</h3>
          <p id="preview${sectionName}"></p>
        </div>
      `;
      previewSection.insertAdjacentHTML('beforeend', previewHTML);

      // Update preview dynamically
      document.getElementById(sectionName.toLowerCase()).addEventListener('input', function() {
        document.getElementById(`preview${sectionName}`).textContent = this.value;
      });
    }

    // Clear Resume
    function clearResume() {
      document.querySelectorAll('input, textarea').forEach(element => {
        element.value = '';
      });
      document.getElementById('dynamicSections').innerHTML = '';
      updatePreview();
    }

    // PDF Download Function
    function downloadPDF() {
      const resume = document.getElementById('resumePreview');
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF('p', 'mm', 'a4');
      
      // Hide download button before capturing
      const downloadBtn = document.querySelector('.download-btn');
      const originalDisplay = downloadBtn.style.display;
      downloadBtn.style.display = 'none';

      html2canvas(resume, { scale: 2, useCORS: true }).then(canvas => {
        const imgData = canvas.toDataURL('image/png', 1.0);
        const imgWidth = 210; // A4 width in mm
        const imgHeight = (canvas.height * imgWidth) / canvas.width;
        doc.addImage(imgData, 'PNG', 0, 0, imgWidth, imgHeight);
        doc.save('resume.pdf');
        downloadBtn.style.display = originalDisplay;
      });
    }
  </script>
</body>
</html> <script type='text/javascript' src='//pl26146723.effectiveratecpm.com/f8/7d/12/f87d123b98862cb5abdddb54a8d11127.js'></script> <script type='text/javascript' src='//pl26146723.effectiveratecpm.com/f8/7d/12/f87d123b98862cb5abdddb54a8d11127.js'></script>
