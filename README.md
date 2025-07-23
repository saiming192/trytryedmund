<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>簡易電商展示頁</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      height: 100vh;
    }

    /* 左邊選單 */
    .sidebar {
      width: 200px;
      background-color: #f0f0f0;
      padding: 20px;
      box-shadow: 2px 0 5px rgba(0,0,0,0.1);
    }

    .sidebar button {
      display: block;
      width: 100%;
      margin-bottom: 10px;
      padding: 10px;
      border: none;
      background-color: #ddd;
      cursor: pointer;
      text-align: left;
    }

    .sidebar button:hover {
      background-color: #ccc;
    }

    /* 右邊內容區 */
    .content {
      flex: 1;
      padding: 40px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .product-image {
      width: 300px;
      height: 200px;
      background-color: #eee;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 20px;
    }

    .product-name {
      font-size: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <!-- 左邊：商品選單 -->
  <div class="sidebar">
    <button onclick="showProduct(1)">商品一</button>
    <button onclick="showProduct(2)">商品二</button>
    <button onclick="showProduct(3)">商品三</button>
    <button onclick="showProduct(4)">商品四</button>
    <button onclick="showProduct(5)">商品五</button>
  </div>

  <!-- 右邊：商品展示 -->
  <div class="content">
    <div class="product-image" id="productImage">圖片區</div>
    <div class="product-name" id="productName">請選擇商品</div>
  </div>

  <!-- JavaScript -->
  <script>
    function showProduct(index) {
      const names = ["商品一", "商品二", "商品三", "商品四", "商品五"];
      const imageUrls = [
        "https://placehold.co/300x200?text=商品一",
        "https://placehold.co/300x200?text=商品二",
        "https://placehold.co/300x200?text=商品三",
        "https://placehold.co/300x200?text=商品四",
        "https://placehold.co/300x200?text=商品五"
      ];

      document.getElementById("productName").textContent = names[index - 1];
      document.getElementById("productImage").innerHTML = `<img src="${imageUrls[index - 1]}" alt="${names[index - 1]}" style="max-width: 100%; max-height: 100%;">`;
    }
  </script>

</body>
</html>

