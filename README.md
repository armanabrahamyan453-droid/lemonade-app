# lemonade-app
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LemonFresh — мини-магазин</title>
<style>
  body { font-family: Arial, sans-serif; background: linear-gradient(135deg,#fff176,#ffd54f); text-align:center; padding:40px; }
  h1 { color:#444; }
  .flavor-btn, .order-btn, .clear-btn { padding:10px 20px; margin:10px; border:none; border-radius:10px; cursor:pointer; font-size:1em; transition:0.3s; }
  .flavor-btn { background:#fff59d; border:2px solid #fdd835; }
  .flavor-btn:hover { background:#fbc02d; color:#fff; }
  .order-btn { background:#fbc02d; }
  .order-btn:hover { background:#f57f17; color:#fff; }
  .clear-btn { background:#e0e0e0; }
  .clear-btn:hover { background:#bdbdbd; }
  .cart { margin-top:20px; font-weight:bold; color:#e65100; }
  img { width:200px; border-radius:20px; box-shadow:0 0 15px rgba(0,0,0,0.3); transition:0.3s; }
  img:hover { transform:scale(1.05); }
</style>
</head>
<body>

<h1>🍋 LemonFresh — мини-магазин</h1>
<img id="drinkImg" src="https://images.unsplash.com/photo-1558642452-9d2a7deb7f62" alt="Лимонад">

<div>
  <button class="flavor-btn" onclick="addToCart('Классический 🍋',400,'https://images.unsplash.com/photo-1558642452-9d2a7deb7f62')">Классический</button>
  <button class="flavor-btn" onclick="addToCart('Малиновый 🍓',450,'https://images.unsplash.com/photo-1600180758890-6b94519a8ba3')">Малиновый</button>
  <button class="flavor-btn" onclick="addToCart('Киви 🥝',450,'https://images.unsplash.com/photo-1613470208854-2a58b8e5fda9')">Киви</button>
  <button class="flavor-btn" onclick="addToCart('Манго 🥭',500,'https://images.unsplash.com/photo-1590080875832-0e24f0b9d6c6')">Манго</button>
</div>

<div class="cart" id="cartText">Корзина пуста</div>
<button class="order-btn" onclick="checkout()">Заказать через Viber</button>
<button class="clear-btn" onclick="clearCart()">Очистить корзину</button>

<script>
let cart = [];

function addToCart(name, price, img){
  cart.push({name, price, img});
  document.getElementById('drinkImg').src = img;
  updateCartText();
}

function updateCartText(){
  if(cart.length===0){
    document.getElementById('cartText').textContent = 'Корзина пуста';
    return;
  }
  let text = 'В корзине:\n';
  let total = 0;
  cart.forEach((item,i)=>{
    text += `${i+1}. ${item.name} — ${item.price} драм\n`;
    total += item.price;
  });
  text += `Итого: ${total} драм`;
  document.getElementById('cartText').textContent = text;
}

function clearCart(){
  cart = [];
  updateCartText();
}

function checkout(){
  if(cart.length===0){
    alert('Корзина пуста! Выберите лимонад.');
    return;
  }
  let message = 'Заказ LemonFresh:\n';
  let total = 0;
  cart.forEach((item,i)=>{
    message += `${i+1}. ${item.name} — ${item.price} драм\n`;
    total += item.price;
  });
  message += `Итого: ${total} драм`;

  const phoneNumber = '+37495610630';
  window.location.href = `viber://chat?number=${encodeURIComponent(phoneNumber)}&text=${encodeURIComponent(message)}`;
}
</script>

</body>
</html>
