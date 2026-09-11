<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Admit Card Portal - Purna Vikash Central School</title>
  <style>
    * { box-sizing: border-box; font-family: 'Segoe UI', Arial, sans-serif; }
    body { background: #f0f2f5; padding: 20px; margin: 0; }
    
    /* Form Styling */
    .container { max-width: 650px; margin: auto; background: #fff; padding: 25px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
    h2 { text-align: center; color: #1a365d; margin-top: 0; }
    .form-group { margin-bottom: 14px; }
    label { display: block; font-weight: 600; margin-bottom: 5px; color: #333; }
    input, select { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 4px; font-size: 14px; }
    .btn { width: 100%; background: #1a365d; color: white; border: none; padding: 12px; font-size: 16px; font-weight: 600; border-radius: 4px; cursor: pointer; margin-top: 10px; }
    .btn:hover { background: #2c5282; }

    /* Admit Card Template (Hidden until generated) */
    #admit-card-container { display: none; max-width: 750px; margin: 30px auto; background: white; padding: 30px; border: 3px double #1a365d; border-radius: 6px; }
    .card-header { text-align: center; border-bottom: 2px solid #1a365d; padding-bottom: 12px; margin-bottom: 20px; }
    .card-header h1 { margin: 0; font-size: 24px; color: #1a365d; text-transform: uppercase; letter-spacing: 0.5px; }
    .card-header p { margin: 4px 0; font-weight: 600; color: #4a5568; }
    .admit-title { display: inline-block; background: #1a365d; color: #fff; padding: 4px 18px; border-radius: 3px; font-size: 14px; text-transform: uppercase; margin-top: 8px; }
    
    .card-body { display: grid; grid-template-columns: 1fr 130px; gap: 20px; margin-bottom: 30px; }
    .details-table { width: 100%; border-collapse: collapse; }
    .details-table td { padding: 7px 4px; font-size: 15px; }
    .details-table td:first-child { font-weight: 600; color: #333; width: 38%; }
    
    .photo-box { width: 120px; height: 140px; border: 1.5px dashed #718096; display: flex; align-items: center; justify-content: center; text-align: center; font-size: 12px; color: #718096; margin-left: auto; }
    .card-footer { display: flex; justify-content: space-between; margin-top: 50px; padding: 0 10px; }
    .sig-line { border-top: 1px solid #333; width: 180px; text-align: center; font-size: 13px; font-weight: 600; padding-top: 6px; }

    .print-actions { text-align: center; margin-top: 20px; display: flex; gap: 10px; justify-content: center; }
    .btn-print { background: #2b6cb0; width: auto; padding: 10px 24px; }
    .btn-reset { background: #718096; width: auto; padding: 10px 24px; }

    /* Print Setup */
    @media print {
      body { background: white; padding: 0; margin: 0; }
      .container, .print-actions { display: none; }
      #admit-card-container { display: block !important; border: 2px solid #000; box-shadow: none; margin: 0; width: 100%; max-width: 100%; }
      .card-header h1 { color: #000; }
      .admit-title { background: #000; -webkit-print-color-adjust: exact; print-color-adjust: exact; }
    }
  </style>
</head>
<body>

<div class="container" id="form-section">
  <h2>Admit Card Entry Portal</h2>
  <form id="admitForm">
    <div class="form-group">
      <label>Candidate Name:</label>
      <input type="text" id="name" required placeholder="Enter student full name">
    </div>
    <div class="form-group">
      <label>Father's / Guardian's Name:</label>
      <input type="text" id="father" required placeholder="Enter father's name">
    </div>
    <div class="form-group">
      <label>Roll Number / Registration No:</label>
      <input type="text" id="roll" required placeholder="Enter roll number">
    </div>
    <div class="form-group">
      <label>Class & Section:</label>
      <input type="text" id="classSec" required placeholder="e.g. Class IX-A or Class X">
    </div>
    <div class="form-group">
      <label>Exam / Assessment Name:</label>
      <input type="text" id="exam" required placeholder="e.g. Annual Examination 2026-27">
    </div>
    <div class="form-group">
      <label>Examination Center:</label>
      <input type="text" id="center" value="Purna Vikash Central School" required>
    </div>
    <button type="submit" class="btn">Generate Admit Card</button>
  </form>
</div>

<!-- Output Admit Card -->
<div id="admit-card-container">
  <div class="card-header">
    <h1>PURNA VIKASH CENTRAL SCHOOL</h1>
    <p>Affiliated to CBSE, New Delhi | Affiliation No. 230130</p>
    <div><span class="admit-title" id="out-exam">EXAMINATION ADMIT CARD</span></div>
  </div>

  <div class="card-body">
    <table class="details-table">
      <tr><td>Roll Number:</td><td><strong id="out-roll"></strong></td></tr>
      <tr><td>Student Name:</td><td><span id="out-name"></span></td></tr>
      <tr><td>Father's Name:</td><td><span id="out-father"></span></td></tr>
      <tr><td>Class & Section:</td><td><span id="out-class"></span></td></tr>
      <tr><td>Exam Center:</td><td><span id="out-center"></span></td></tr>
    </table>
    <div class="photo-box">Affix Student Photograph Here</div>
  </div>

  <div class="card-footer">
    <div class="sig-line">Candidate Signature</div>
    <div class="sig-line">Class Teacher</div>
    <div class="sig-line">Headmistress / Principal</div>
  </div>

  <div class="print-actions">
    <button class="btn btn-print" onclick="window.print()">Print / Save PDF</button>
    <button class="btn btn-reset" onclick="location.reload()">Create Another</button>
  </div>
</div>

<script>
  const form = document.getElementById('admitForm');
  form.addEventListener('submit', function(e) {
    e.preventDefault();

    document.getElementById('out-name').textContent = document.getElementById('name').value.toUpperCase();
    document.getElementById('out-father').textContent = document.getElementById('father').value.toUpperCase();
    document.getElementById('out-roll').textContent = document.getElementById('roll').value;
    document.getElementById('out-class').textContent = document.getElementById('classSec').value;
    document.getElementById('out-exam').textContent = document.getElementById('exam').value.toUpperCase();
    document.getElementById('out-center').textContent = document.getElementById('center').value;

    document.getElementById('form-section').style.display = 'none';
    document.getElementById('admit-card-container').style.display = 'block';
  });
</script>

</body>
</html>[ID card app.txt](https://github.com/user-attachments/files/32086779/ID.card.app.txt)
