<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EXELANS TATTOO - Randevu Sistemi</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(135deg, #0D1546 0%, #02020B 100%); min-height: 100vh; padding: 20px; }
        .logo-header { text-align: center; margin-bottom: 30px; padding: 30px; background: white; border-radius: 15px; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3); max-width: 1800px; margin: 0 auto 30px auto; }
        .logo-header h1 { font-size: 4em; font-weight: bold; color: #02020B; margin: 0; letter-spacing: 2px; }
        .container { max-width: 1800px; margin: 0 auto; background: white; border-radius: 20px; box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5); padding: 40px; }
        h1 { text-align: center; color: #02020B; margin-bottom: 30px; font-size: 2.5em; }
        .stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; margin-bottom: 30px; }
        .stat-card { background: linear-gradient(135deg, #2D4882 0%, #0D1546 100%); color: white; padding: 20px; border-radius: 12px; text-align: center; border: 2px solid #5271A1; }
        .stat-card h3 { font-size: 2em; margin-bottom: 5px; }
        .stat-card p { opacity: 0.9; }
        .controls { display: flex; gap: 15px; margin-bottom: 30px; flex-wrap: wrap; }
        .search-box { flex: 1; min-width: 250px; }
        .search-box input { width: 100%; padding: 12px 15px; border: 2px solid #e0e0e0; border-radius: 8px; font-size: 16px; }
        .search-box input:focus { outline: none; border-color: #2D4882; }
        .btn { padding: 12px 24px; border: none; border-radius: 8px; font-size: 16px; font-weight: 600; cursor: pointer; transition: all 0.3s; }
        .btn-primary { background: linear-gradient(135deg, #2D4882 0%, #0D1546 100%); color: white; border: 2px solid #5271A1; }
        .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(45, 72, 130, 0.6); }
        .btn-success { background: #10b981; color: white; }
        .btn-danger { background: #ef4444; color: white; }
        .btn-warning { background: #f59e0b; color: white; }
        .btn-small { padding: 6px 12px; font-size: 14px; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.5); z-index: 1000; justify-content: center; align-items: center; }
        .modal.active { display: flex; }
        .modal-content { background: white; border-radius: 15px; padding: 30px; max-width: 600px; width: 90%; max-height: 90vh; overflow-y: auto; }
        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .close-btn { background: none; border: none; font-size: 28px; cursor: pointer; color: #999; }
        .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 20px; }
        .form-group { margin-bottom: 20px; }
        .form-group label { display: block; margin-bottom: 8px; color: #555; font-weight: 600; }
        .form-group input, .form-group select, .form-group textarea { width: 100%; padding: 12px 15px; border: 2px solid #e0e0e0; border-radius: 8px; font-size: 16px; font-family: inherit; }
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus { outline: none; border-color: #2D4882; }
        .image-upload-area { border: 2px dashed #e0e0e0; border-radius: 8px; padding: 20px; text-align: center; cursor: pointer; }
        .image-upload-area:hover { border-color: #2D4882; background: #f9fafb; }
        .uploaded-image-preview { max-width: 100%; max-height: 200px; border-radius: 8px; margin-top: 10px; }
        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        thead { background: linear-gradient(135deg, #2D4882 0%, #0D1546 100%); color: white; }
        th, td { padding: 15px; text-align: left; border-bottom: 1px solid #e0e0e0; }
        th { font-weight: 600; cursor: pointer; }
        tbody tr:hover { background: #f9fafb; }
        .status-badge { display: inline-block; padding: 5px 12px; border-radius: 20px; font-size: 14px; font-weight: 600; }
        .status-bekliyor { background: #fef3c7; color: #92400e; }
        .status-onaylandi { background: #d1fae5; color: #065f46; }
        .status-tamamlandi { background: #dbeafe; color: #1e40af; }
        .status-iptal { background: #fee2e2; color: #991b1b; }
        .session-badge { display: inline-block; padding: 5px 12px; border-radius: 20px; font-size: 13px; font-weight: 600; background: #dbeafe; color: #1e40af; }
        .session-complete { background: #d1fae5; color: #065f46; }
        .session-progress { background: #fef3c7; color: #92400e; }
        .deposit-badge { display: inline-block; padding: 3px 8px; border-radius: 12px; font-size: 12px; font-weight: 600; }
        .deposit-paid { background: #d1fae5; color: #065f46; }
        .deposit-unpaid { background: #fee2e2; color: #991b1b; }
        .image-preview { max-width: 80px; max-height: 80px; border-radius: 8px; cursor: pointer; border: 2px solid #e0e0e0; }
        .action-buttons { display: flex; gap: 8px; flex-wrap: wrap; }
        .price-info { color: #059669; font-weight: 600; }
        .checkbox-group { display: flex; align-items: center; gap: 10px; }
        @media (max-width: 768px) { .logo-header h1 { font-size: 2.5em; } }
    </style>
</head>
<body>
    <div class="logo-header">
        <h1>EXELANS TATTOO</h1>
    </div>
    
    <div class="container">
        <h1>📅 Randevu Yönetim Sistemi</h1>
        <div class="stats">
            <div class="stat-card"><h3 id="totalAppointments">0</h3><p>Toplam Randevu</p></div>
            <div class="stat-card"><h3 id="todayAppointments">0</h3><p>Bugünkü Randevular</p></div>
            <div class="stat-card"><h3 id="pendingAppointments">0</h3><p>Bekleyen Randevular</p></div>
        </div>
        <div class="controls">
            <div class="search-box"><input type="text" id="searchInput" placeholder="🔍 Müşteri adı, telefon veya not ara..."></div>
            <select id="statusFilter" class="btn">
                <option value="">Tüm Durumlar</option>
                <option value="bekliyor">Bekliyor</option>
                <option value="onaylandi">Onaylandı</option>
                <option value="tamamlandi">Tamamlandı</option>
                <option value="iptal">İptal</option>
            </select>
            <button class="btn btn-primary" onclick="openModal()">➕ Yeni Randevu</button>
        </div>
        <div class="table-container">
            <table id="appointmentsTable">
                <thead>
                    <tr>
                        <th onclick="sortTable('date')">Tarih & Saat ⇅</th>
                        <th onclick="sortTable('customer')">Müşteri ⇅</th>
                        <th onclick="sortTable('phone')">Telefon ⇅</th>
                        <th onclick="sortTable('service')">Hizmet ⇅</th>
                        <th onclick="sortTable('status')">Durum ⇅</th>
                        <th>Seans</th>
                        <th>Fiyat</th>
                        <th>Kapora</th>
                        <th>Görsel</th>
                        <th>Notlar</th>
                        <th>İşlemler</th>
                    </tr>
                </thead>
                <tbody id="appointmentsBody"></tbody>
            </table>
        </div>
    </div>
    <div id="appointmentModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="modalTitle">Yeni Randevu</h2>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <form id="appointmentForm" onsubmit="saveAppointment(event)">
                <input type="hidden" id="appointmentId">
                <div class="form-row">
                    <div class="form-group"><label for="customerName">İsim *</label><input type="text" id="customerName" required placeholder="Örn: Ahmet"></div>
                    <div class="form-group"><label for="customerSurname">Soyisim *</label><input type="text" id="customerSurname" required placeholder="Örn: Yılmaz"></div>
                </div>
                <div class="form-group"><label for="customerPhone">Telefon *</label><input type="tel" id="customerPhone" required placeholder="0555 123 45 67"></div>
                <div class="form-row">
                    <div class="form-group"><label for="appointmentDate">Tarih *</label><input type="date" id="appointmentDate" required></div>
                    <div class="form-group"><label for="appointmentTime">Saat *</label>
                        <select id="appointmentTime" required>
                            <option value="">Seçiniz</option>
                            <option value="13:00">13:00</option><option value="13:30">13:30</option><option value="14:00">14:00</option><option value="14:30">14:30</option>
                            <option value="15:00">15:00</option><option value="15:30">15:30</option><option value="16:00">16:00</option><option value="16:30">16:30</option>
                            <option value="17:00">17:00</option><option value="17:30">17:30</option><option value="18:00">18:00</option><option value="18:30">18:30</option>
                            <option value="19:00">19:00</option><option value="19:30">19:30</option><option value="20:00">20:00</option><option value="20:30">20:30</option>
                            <option value="21:00">21:00</option>
                        </select>
                    </div>
                </div>
                <div class="form-group"><label for="serviceType">Hizmet Türü *</label>
                    <select id="serviceType" required>
                        <option value="">Seçiniz</option>
                        <option value="Tasarım">Tasarım</option>
                        <option value="Dövme">Dövme</option>
                        <option value="Cover up">Cover up</option>
                        <option value="Touch up">Touch up</option>
                        <option value="Rütuş">Rütuş</option>
                        <option value="Kontrol">Kontrol</option>
                        <option value="Diğer">Diğer</option>
                    </select>
                </div>
                <div class="form-row">
                    <div class="form-group"><label for="totalSessions">Toplam Seans</label>
                        <select id="totalSessions">
                            <option value="1">Tek Seans</option>
                            <option value="2">2 Seans</option>
                            <option value="3">3 Seans</option>
                            <option value="4">4 Seans</option>
                            <option value="5">5 Seans</option>
                            <option value="6">6 Seans</option>
                            <option value="7">7 Seans</option>
                            <option value="8">8 Seans</option>
                            <option value="9">9 Seans</option>
                            <option value="10">10 Seans</option>
                        </select>
                    </div>
                    <div class="form-group"><label for="completedSessions">Tamamlanan Seans</label>
                        <select id="completedSessions">
                            <option value="0">0</option>
                            <option value="1">1</option>
                            <option value="2">2</option>
                            <option value="3">3</option>
                            <option value="4">4</option>
                            <option value="5">5</option>
                            <option value="6">6</option>
                            <option value="7">7</option>
                            <option value="8">8</option>
                            <option value="9">9</option>
                            <option value="10">10</option>
                        </select>
                    </div>
                </div>
                <div class="form-group"><label for="appointmentStatus">Durum *</label>
                    <select id="appointmentStatus" required>
                        <option value="bekliyor">Bekliyor</option>
                        <option value="onaylandi">Onaylandı</option>
                        <option value="tamamlandi">Tamamlandı</option>
                        <option value="iptal">İptal</option>
                    </select>
                </div>
                <div class="form-row">
                    <div class="form-group"><label for="totalPrice">İşlem Fiyatı (₺)</label><input type="number" id="totalPrice" min="0" step="0.01" placeholder="0.00"></div>
                    <div class="form-group"><label for="depositAmount">Kapora Miktarı (₺)</label><input type="number" id="depositAmount" min="0" step="0.01" placeholder="0.00"></div>
                </div>
                <div class="form-group">
                    <div class="checkbox-group"><input type="checkbox" id="depositPaid"><label for="depositPaid" style="margin: 0;">Kapora Alındı</label></div>
                </div>
                <div class="form-group"><label>Görsel Yükle</label>
                    <div class="image-upload-area" id="imageUploadArea" onclick="document.getElementById('imageInput').click()">
                        <p>📷 Görsel yüklemek için tıklayın</p>
                        <img id="imagePreview" class="uploaded-image-preview" style="display: none;">
                    </div>
                    <input type="file" id="imageInput" accept="image/*" style="display: none;" onchange="handleImageUpload(event)">
                </div>
                <div class="form-group"><label for="appointmentNotes">Notlar</label><textarea id="appointmentNotes" placeholder="Ek bilgiler veya notlar..."></textarea></div>
                <div style="display: flex; gap: 10px; margin-top: 25px;">
                    <button type="submit" class="btn btn-success" style="flex: 1;">💾 Kaydet</button>
                    <button type="button" class="btn btn-danger" onclick="closeModal()" style="flex: 1;">❌ İptal</button>
                </div>
            </form>
        </div>
    </div>
    <script>
        let appointments = [], editingId = null, sortColumn = 'date', sortDirection = 'asc', currentImage = null;
        function loadAppointments() { const stored = localStorage.getItem('appointments'); if (stored) appointments = JSON.parse(stored); renderAppointments(); updateStats(); }
        function saveToStorage() { localStorage.setItem('appointments', JSON.stringify(appointments)); }
        function handleImageUpload(event) { const file = event.target.files[0]; if (file) { const reader = new FileReader(); reader.onload = function(e) { currentImage = e.target.result; document.getElementById('imagePreview').src = currentImage; document.getElementById('imagePreview').style.display = 'block'; document.getElementById('imageUploadArea').classList.add('has-image'); }; reader.readAsDataURL(file); } }
        function openModal(id = null) { const modal = document.getElementById('appointmentModal'); document.getElementById('appointmentForm').reset(); document.getElementById('imagePreview').style.display = 'none'; currentImage = null; editingId = id; if (id) { document.getElementById('modalTitle').textContent = 'Randevu Düzenle'; const a = appointments.find(x => x.id === id); if (a) { document.getElementById('customerName').value = a.name || ''; document.getElementById('customerSurname').value = a.surname || ''; document.getElementById('customerPhone').value = a.phone; document.getElementById('appointmentDate').value = a.date; document.getElementById('appointmentTime').value = a.time; document.getElementById('serviceType').value = a.service; document.getElementById('totalSessions').value = a.totalSessions || 1; document.getElementById('completedSessions').value = a.completedSessions || 0; document.getElementById('appointmentStatus').value = a.status; document.getElementById('totalPrice').value = a.totalPrice || ''; document.getElementById('depositAmount').value = a.depositAmount || ''; document.getElementById('depositPaid').checked = a.depositPaid || false; document.getElementById('appointmentNotes').value = a.notes || ''; if (a.image) { currentImage = a.image; document.getElementById('imagePreview').src = currentImage; document.getElementById('imagePreview').style.display = 'block'; } } } else { document.getElementById('modalTitle').textContent = 'Yeni Randevu'; document.getElementById('appointmentDate').value = new Date().toISOString().split('T')[0]; } modal.classList.add('active'); }
        function closeModal() { document.getElementById('appointmentModal').classList.remove('active'); editingId = null; currentImage = null; }
        function saveAppointment(event) { event.preventDefault(); const name = document.getElementById('customerName').value; const surname = document.getElementById('customerSurname').value; const appointment = { id: editingId || Date.now().toString(), name: name, surname: surname, customer: name + ' ' + surname, phone: document.getElementById('customerPhone').value, date: document.getElementById('appointmentDate').value, time: document.getElementById('appointmentTime').value, service: document.getElementById('serviceType').value, totalSessions: parseInt(document.getElementById('totalSessions').value) || 1, completedSessions: parseInt(document.getElementById('completedSessions').value) || 0, status: document.getElementById('appointmentStatus').value, totalPrice: parseFloat(document.getElementById('totalPrice').value) || 0, depositAmount: parseFloat(document.getElementById('depositAmount').value) || 0, depositPaid: document.getElementById('depositPaid').checked, image: currentImage, notes: document.getElementById('appointmentNotes').value, createdAt: editingId ? appointments.find(a => a.id === editingId).createdAt : new Date().toISOString() }; if (editingId) { const index = appointments.findIndex(a => a.id === editingId); appointments[index] = appointment; } else { appointments.push(appointment); } saveToStorage(); renderAppointments(); updateStats(); closeModal(); }
        function deleteAppointment(id) { if (confirm('Bu randevuyu silmek istediğinizden emin misiniz?')) { appointments = appointments.filter(a => a.id !== id); saveToStorage(); renderAppointments(); updateStats(); } }
        function viewImage(imageData) { if (imageData) { const win = window.open(); win.document.write('<img src="' + imageData + '" style="max-width:100%; height:auto;">'); } }
        function renderAppointments() { const tbody = document.getElementById('appointmentsBody'); const searchTerm = document.getElementById('searchInput').value.toLowerCase(); const statusFilter = document.getElementById('statusFilter').value; let filtered = appointments.filter(a => { const matchesSearch = a.customer.toLowerCase().includes(searchTerm) || a.phone.includes(searchTerm) || (a.notes && a.notes.toLowerCase().includes(searchTerm)); const matchesStatus = !statusFilter || a.status === statusFilter; return matchesSearch && matchesStatus; }); filtered.sort((a, b) => { let aVal, bVal; switch(sortColumn) { case 'date': aVal = new Date(a.date + ' ' + a.time); bVal = new Date(b.date + ' ' + b.time); break; case 'customer': aVal = a.customer.toLowerCase(); bVal = b.customer.toLowerCase(); break; case 'phone': aVal = a.phone; bVal = b.phone; break; case 'service': aVal = a.service.toLowerCase(); bVal = b.service.toLowerCase(); break; case 'status': aVal = a.status; bVal = b.status; break; default: return 0; } if (aVal < bVal) return sortDirection === 'asc' ? -1 : 1; if (aVal > bVal) return sortDirection === 'asc' ? 1 : -1; return 0; }); tbody.innerHTML = filtered.map(a => { const dateObj = new Date(a.date); const formattedDate = dateObj.toLocaleDateString('tr-TR', { day: '2-digit', month: '2-digit', year: 'numeric' }); const totalSessions = a.totalSessions || 1; const completedSessions = a.completedSessions || 0; let sessionBadgeClass = 'session-badge'; if (completedSessions === totalSessions) sessionBadgeClass += ' session-complete'; else if (completedSessions > 0) sessionBadgeClass += ' session-progress'; const sessionInfo = totalSessions > 1 ? `<span class="${sessionBadgeClass}">${completedSessions}/${totalSessions}</span>` : '-'; const priceInfo = a.totalPrice > 0 ? `<span class="price-info">${a.totalPrice.toFixed(2)} ₺</span>` : '-'; const depositInfo = a.depositPaid && a.depositAmount > 0 ? `<span class="deposit-badge deposit-paid">✓ ${a.depositAmount.toFixed(2)} ₺</span>` : a.depositAmount > 0 ? `<span class="deposit-badge deposit-unpaid">✗ ${a.depositAmount.toFixed(2)} ₺</span>` : '<span class="deposit-badge deposit-unpaid">✗ Yok</span>'; const imageCell = a.image ? `<img src="${a.image}" class="image-preview" onclick="viewImage('${a.image}')" alt="Randevu görseli">` : '-'; return `<tr><td><strong>${formattedDate}</strong><br>${a.time}</td><td>${a.customer}</td><td>${a.phone}</td><td>${a.service}</td><td><span class="status-badge status-${a.status}">${getStatusText(a.status)}</span></td><td>${sessionInfo}</td><td>${priceInfo}</td><td>${depositInfo}</td><td>${imageCell}</td><td>${a.notes || '-'}</td><td><div class="action-buttons"><button class="btn btn-warning btn-small" onclick="openModal('${a.id}')">✏️ Düzenle</button><button class="btn btn-danger btn-small" onclick="deleteAppointment('${a.id}')">🗑️ Sil</button></div></td></tr>`; }).join(''); }
        function getStatusText(status) { const statusMap = { 'bekliyor': 'Bekliyor', 'onaylandi': 'Onaylandı', 'tamamlandi': 'Tamamlandı', 'iptal': 'İptal' }; return statusMap[status] || status; }
        function sortTable(column) { if (sortColumn === column) { sortDirection = sortDirection === 'asc' ? 'desc' : 'asc'; } else { sortColumn = column; sortDirection = 'asc'; } renderAppointments(); }
        function updateStats() { const today = new Date().toISOString().split('T')[0]; document.getElementById('totalAppointments').textContent = appointments.length; document.getElementById('todayAppointments').textContent = appointments.filter(a => a.date === today).length; document.getElementById('pendingAppointments').textContent = appointments.filter(a => a.status === 'bekliyor').length; }
        document.getElementById('searchInput').addEventListener('input', renderAppointments);
        document.getElementById('statusFilter').addEventListener('change', renderAppointments);
        document.getElementById('appointmentModal').addEventListener('click', function(e) { if (e.target === this) closeModal(); });
        window.onload = loadAppointments;
    </script>
</body>
</html>
