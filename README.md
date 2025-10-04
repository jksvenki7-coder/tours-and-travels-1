# tours-and-travels-1<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Tours & Travels Booking Form</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f0f8ff;
    color: #003366;
    margin: 0;
    padding: 20px;
  }
  h1 {
    color: #0077cc;
    text-align: center;
  }
  form {
    max-width: 600px;
    margin: 0 auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px #aaccee;
  }
  label {
    font-weight: bold;
    display: block;
    margin-top: 15px;
  }
  input[type="text"],
  input[type="tel"],
  input[type="number"],
  select,
  textarea {
    width: 100%;
    padding: 8px;
    margin-top: 6px;
    border-radius: 4px;
    border: 1px solid #0077cc;
    box-sizing: border-box;
  }
  textarea {
    resize: vertical;
    height: 60px;
  }
  input[type="file"] {
    margin-top: 6px;
  }
  button {
    margin-top: 20px;
    background-color: #0077cc;
    border: none;
    color: white;
    padding: 12px 20px;
    text-align: center;
    font-size: 16px;
    border-radius: 6px;
    cursor: pointer;
    width: 100%;
  }
  button:hover {
    background-color: #005fa3;
  }
  small {
    color: #333;
  }
</style>
</head>
<body>
  <h1>Tours & Travels Booking Form</h1>
  <form id="bookingForm">
    <label for="name">Name *</label>
    <input type="text" id="name" name="name" required />

    <label for="mobile">Mobile Number *</label>
    <input type="tel" id="mobile" name="mobile" pattern="[0-9]{10}" required placeholder="10 digit mobile number" />

    <label for="persons">Number of Persons *</label>
    <input type="number" id="persons" name="persons" min="1" max="20" required />

    <label for="from">From (Place) *</label>
    <input type="text" id="from" name="from" required />

    <label for="to">To (Place) *</label>
    <input type="text" id="to" name="to" required />

    <label for="address">Address *</label>
    <textarea id="address" name="address" required placeholder="Pickup address"></textarea>

    <label for="tourType">Tour/Travel Type *</label>
    <select id="tourType" name="tourType" required onchange="showVehicleOptions()">
      <option value="">Select</option>
      <option value="Monthly Tour">Monthly Tour</option>
      <option value="Family Tour">Family Tour</option>
      <option value="Couple Tour">Couple Tour</option>
      <option value="Daily Tour">Daily Tour</option>
      <option value="Self Travel">Self Travel</option>
      <option value="Travel With Driver">Travel With Driver</option>
      <option value="Ticket Booking">Ticket Booking</option>
    </select>

    <div id="vehicleOptions" style="display:none; margin-top:15px;">
      <label for="vehicleType">Vehicle Type</label>
      <select id="vehicleType" name="vehicleType">
        <option value="">Select</option>
        <option value="Bike">Bike</option>
        <option value="Auto">Auto</option>
        <option value="Car">Car</option>
        <option value="Bus">Bus</option>
        <option value="Tempo">Tempo</option>
        <option value="Taxi">Taxi</option>
      </select>
    </div>

    <label for="message">Additional Details / Message</label>
    <textarea id="message" name="message" placeholder="Any special requests or details"></textarea>

    <label for="photo">Upload Photo (Optional)</label>
    <input type="file" id="photo" name="photo" accept="image/*" capture="environment" />

    <button type="submit">Submit Booking via WhatsApp</button>
    <small>* Required fields</small>
  </form>

  <script>
    const form = document.getElementById('bookingForm');
    const vehicleSection = document.getElementById('vehicleOptions');

    function showVehicleOptions() {
      const tourType = document.getElementById('tourType').value;
      if (tourType === 'Self Travel') {
        vehicleSection.style.display = 'block';
        document.getElementById('vehicleType').setAttribute('required', 'required');
      } else {
        vehicleSection.style.display = 'none';
        document.getElementById('vehicleType').removeAttribute('required');
      }
    }

    form.addEventListener('submit', function(event) {
      event.preventDefault();

      const name = encodeURIComponent(form.name.value.trim());
      const mobile = encodeURIComponent(form.mobile.value.trim());
      const persons = encodeURIComponent(form.persons.value.trim());
      const fromPlace = encodeURIComponent(form.from.value.trim());
      const toPlace = encodeURIComponent(form.to.value.trim());
      const address = encodeURIComponent(form.address.value.trim());
      const tourType = encodeURIComponent(form.tourType.value);
      const vehicleType = form.vehicleType.value ? encodeURIComponent(form.vehicleType.value) : 'N/A';
      const message = form.message.value ? encodeURIComponent(form.message.value.trim()) : 'No additional details';
      
      const photo = form.photo.files.length > 0 ? 'Yes (attached separately)' : 'No';

      const whatsappMsg =
        `*Tours & Travels Booking Request*%0A` +
        `Name: ${name}%0A` +
        `Mobile: ${mobile}%0A` +
        `Number of Persons: ${persons}%0A` +
        `From: ${fromPlace}%0A` +
        `To: ${toPlace}%0A` +
        `Address: ${address}%0A` +
        `Tour/Travel Type: ${tourType}%0A` +
        `Vehicle Type: ${vehicleType}%0A` +
        `Additional Details: ${message}%0A` +
        `Photo Provided: ${photo}`;

      const whatsappNumber = '919877143043';

      const whatsappURL = `https://wa.me/${whatsappNumber}?text=${whatsappMsg}`;

      window.open(whatsappURL, '_blank');
    });
  </script>
</body>
</html>
