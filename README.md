<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gran Forno - Palmas/TO</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&family=Bebas+Neue&display=swap');
        
        :root {
            --appetite-red: #d90429;
            --value-yellow: #ffb703;
            --night-black: #0b090a;
        }

        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background-color: #f8f9fa;
            color: #1a1a1a;
        }

        .font-bebas { font-family: 'Bebas Neue', cursive; }

        .hero-gradient {
            background: linear-gradient(180deg, var(--night-black) 0%, #3a0a0a 100%);
        }

        .btn-order {
            background-color: var(--appetite-red);
            box-shadow: 0 4px 15px rgba(217, 4, 41, 0.4);
        }

        .combo-gold {
            background: white;
            border-left: 5px solid var(--value-yellow);
        }

        .location-badge {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(5px);
        }

        /* Estilo para o contador de visualização */
        .view-counter {
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
    </style>
</head>
<body class="pb-28">

    <!-- Contador de Pessoas Online (Olho) -->
    <div class="fixed top-4 right-4 z-50 view-counter px-3 py-1.5 rounded-full flex items-center gap-2 shadow-lg animate-pulse">
        <i class="fas fa-eye text-red-500 text-[10px]"></i>
        <span id="online-count" class="text-[10px] text-white font-bold"></span>
    </div>

    <!-- Header com Localização -->
    <header class="hero-gradient text-white pt-8 pb-14 px-6 rounded-b-[3.5rem] shadow-2xl relative overflow-hidden">
        <div class="flex flex-col items-center relative z-10">
            <div class="location-badge px-4 py-1.5 rounded-full flex items-center gap-2 mb-4 animate-bounce">
                <i class="fas fa-map-marker-alt text-red-500"></i>
                <span class="text-[10px] font-bold tracking-widest uppercase">Palmas - Tocantins</span>
            </div>
            
            <h1 class="font-bebas text-6xl tracking-tighter italic leading-none">GRAN FORNO</h1>
            <p class="text-[11px] tracking-[0.4em] text-yellow-400 font-black uppercase mt-2">Pizzaria Artesanal</p>
        </div>
        
        <div class="absolute -right-10 -bottom-10 opacity-10">
            <i class="fas fa-pizza-slice text-[150px] rotate-12"></i>
        </div>
    </header>

    <!-- Seção de Ofertas -->
    <div class="px-5 -mt-8 space-y-4">
        
        <!-- COMBO 1: DESTAQUE -->
        <div class="bg-white p-5 rounded-[2.5rem] shadow-xl border border-red-50 relative overflow-hidden">
            <div class="flex justify-between items-start">
                <div>
                    <span class="bg-red-600 text-white text-[9px] font-black px-3 py-1 rounded-full uppercase">Oferta do Dia</span>
                    <h4 class="font-bebas text-3xl text-gray-900 mt-2 leading-none">COMBO GALERA</h4>
                    <p class="text-xs text-gray-500 font-medium mt-1">1 Pizza G + Refri 1.5L</p>
                    <p class="text-[9px] text-orange-600 font-bold mt-1">* + R$ 10 p/ Carne de Sol</p>
                </div>
                <div class="text-right">
                    <span class="text-3xl font-black text-red-600 italic">R$ 60</span>
                </div>
            </div>
            <button onclick="fazerPedido('Combo Galera de R$ 60')" class="w-full mt-4 btn-order text-white py-4 rounded-2xl font-bold text-sm uppercase tracking-widest transition-transform active:scale-95">
                Eu quero esse!
            </button>
        </div>

        <!-- OUTROS COMBOS -->
        <div class="grid grid-cols-2 gap-4">
            <div class="combo-gold p-4 rounded-3xl shadow-md flex flex-col justify-between">
                <div>
                    <h4 class="font-bebas text-xl text-gray-800">COMBO DUPLO</h4>
                    <p class="text-[9px] text-gray-400 leading-tight uppercase font-bold">2 Pizzas G + Refri</p>
                </div>
                <div class="mt-4">
                    <span class="text-2xl font-black text-slate-900 leading-none">R$ 90</span>
                    <button onclick="fazerPedido('Combo Duplo de R$ 90')" class="w-full mt-2 text-[10px] font-black text-red-600 uppercase py-2 bg-red-50 rounded-xl">Pedir</button>
                </div>
            </div>

            <div class="combo-gold p-4 rounded-3xl shadow-md flex flex-col justify-between">
                <div>
                    <h4 class="font-bebas text-xl text-gray-800">FAMÍLIA PLUS</h4>
                    <p class="text-[9px] text-gray-400 leading-tight uppercase font-bold">3 Pizzas G + 2 Refris</p>
                </div>
                <div class="mt-4">
                    <span class="text-2xl font-black text-slate-900 leading-none">R$ 120</span>
                    <button onclick="fazerPedido('Combo Família Plus de R$ 120')" class="w-full mt-2 text-[10px] font-black text-red-600 uppercase py-2 bg-red-50 rounded-xl">Pedir</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Sabores Famosos -->
    <div class="mt-10 px-6">
        <div class="flex items-center justify-between mb-4">
            <h3 class="font-bebas text-2xl text-gray-800 tracking-wide">SABORES EM DESTAQUE</h3>
            <span class="h-[2px] flex-grow mx-4 bg-gray-200"></span>
        </div>
        <div id="pizzas-list" class="space-y-3"></div>
    </div>

    <!-- Seção de Bebidas -->
    <div class="mt-10 px-6">
        <div class="flex items-center justify-between mb-4">
            <h3 class="font-bebas text-2xl text-gray-800 tracking-wide">BEBIDAS GELADAS</h3>
            <span class="h-[2px] flex-grow mx-4 bg-gray-200"></span>
        </div>
        
        <div class="space-y-3">
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between group" onclick="fazerPedido('Guaraná Antarctica 1.5L')">
                <div class="flex items-center gap-4">
                    <div class="w-10 h-10 bg-green-50 rounded-full flex items-center justify-center">
                        <i class="fas fa-bottle-water text-green-600"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-xs text-gray-800 uppercase">Guaraná Antarctica 1.5L</h4>
                        <p class="text-[9px] text-red-500 font-bold">R$ 12</p>
                    </div>
                </div>
                <i class="fab fa-whatsapp text-green-500"></i>
            </div>

            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between" onclick="fazerPedido('Kuat 2L')">
                <div class="flex items-center gap-4">
                    <div class="w-10 h-10 bg-orange-50 rounded-full flex items-center justify-center">
                        <i class="fas fa-bottle-water text-orange-600"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-xs text-gray-800 uppercase">Kuat 2L</h4>
                        <p class="text-[9px] text-gray-400 font-medium">R$ 10</p>
                    </div>
                </div>
                <i class="fab fa-whatsapp text-green-500"></i>
            </div>
        </div>
    </div>

    <!-- Floating Footer -->
    <div class="fixed bottom-6 left-0 right-0 px-6 z-40">
        <a href="https://wa.me/5563984498256?text=Olá! Gostaria de fazer um pedido." class="w-full bg-[#25D366] text-white h-16 rounded-2xl shadow-2xl flex items-center justify-between px-6 active:scale-95 transition-all">
            <div class="flex items-center gap-3">
                <i class="fab fa-whatsapp text-2xl"></i>
                <div class="text-left">
                    <p class="text-[10px] uppercase font-bold opacity-80 leading-none">Chamar no Whatsapp</p>
                    <p class="font-black text-sm uppercase">Palmas - TO</p>
                </div>
            </div>
            <i class="fas fa-arrow-right animate-pulse"></i>
        </a>
    </div>

    <script>
        const whatsappNumber = "5563984498256";

        const cardapio = [
            { nome: "Calabresa com Cebola", preco: 55, popular: true, maisVendida: true },
            { nome: "Frango com Catupiry", preco: 55, popular: false, maisVendida: false },
            { nome: "Portuguesa Tradicional", preco: 55, popular: true, maisVendida: false },
            { nome: "Muçarela Especial", preco: 55, popular: false, maisVendida: false },
            { nome: "Napolitana", preco: 55, popular: false, maisVendida: false },
            { nome: "Bacon com Milho", preco: 55, popular: false, maisVendida: false },
            { nome: "Marguerita", preco: 55, popular: false, maisVendida: false },
            { nome: "Carne de Sol", preco: 65, popular: true, maisVendida: true }
        ];

        function fazerPedido(item) {
            const mensagem = `Olá Gran Forno! Gostaria de pedir: ${item}`;
            const url = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(mensagem)}`;
            window.location.href = url;
        }

        function render() {
            // Contador aleatório de 2 a 12
            const randomCount = Math.floor(Math.random() * (12 - 2 + 1)) + 2;
            document.getElementById('online-count').innerText = `${randomCount} PESSOAS VENDO AGORA`;

            const container = document.getElementById('pizzas-list');
            container.innerHTML = cardapio.map(p => `
                <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex items-center justify-between active:bg-gray-50 transition-colors" onclick="fazerPedido('${p.nome} - R$ ${p.preco}')">
                    <div class="flex-grow">
                        <div class="flex items-center gap-2 flex-wrap">
                            <h4 class="font-bold text-xs text-gray-800 uppercase ${p.nome === 'Carne de Sol' ? 'text-orange-600' : ''}">${p.nome}</h4>
                            ${p.maisVendida ? '<span class="bg-orange-100 text-orange-600 text-[8px] font-black px-2 py-0.5 rounded-md uppercase">Mais Vendida</span>' : ''}
                        </div>
                        <p class="text-[9px] text-gray-400 font-medium italic">Toque para pedir no Whatsapp</p>
                    </div>
                    <div class="flex items-center gap-3">
                        <div class="bg-slate-50 px-3 py-1 rounded-lg">
                            <span class="text-sm font-black text-red-600">R$ ${p.preco}</span>
                        </div>
                        <i class="fab fa-whatsapp text-green-500 text-lg"></i>
                    </div>
                </div>
            `).join('');
        }

        window.onload = render;
    </script>
</body>
</html>
