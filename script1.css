const stripe1 = document.getElementById("stripe1");
const stripe2 = document.getElementById("stripe2");
const stripe3 = document.getElementById("stripe3");
const stripe4 = document.getElementById("stripe4");
const palette = document.getElementById("palette");
const paletteTitle = document.getElementById("paletteTitle");
const paletteOptions = document.getElementById("paletteOptions");
const closePalette = document.getElementById("closePalette");
const result = document.getElementById("result");

const digitColors = [
  { name: "Czarny", value: 0, css: "#111111" },
  { name: "Br¹zowy", value: 1, css: "#7a3e1d" },
  { name: "Czerwony", value: 2, css: "#c62828" },
  { name: "Pomarañczowy", value: 3, css: "#ef6c00" },
  { name: "¯ó³ty", value: 4, css: "#fdd835" },
  { name: "Zielony", value: 5, css: "#2e7d32" },
  { name: "Niebieski", value: 6, css: "#1565c0" },
  { name: "Fioletowy", value: 7, css: "#6a1b9a" },
  { name: "Szary", value: 8, css: "#757575" },
  { name: "Bia³y", value: 9, css: "#f5f5f5" }
];

const multiplierColors = [
  { name: "Srebrny", value: 0.01, css: "#b0bec5" },
  { name: "Z³oty", value: 0.1, css: "#c9a227" },
  ...digitColors.map((c) => ({ name: c.name, value: 10 ** c.value, css: c.css }))
];

const toleranceColors = [
  { name: "Br¹zowy", value: 1, css: "#7a3e1d" },
  { name: "Czerwony", value: 2, css: "#c62828" },
  { name: "Zielony", value: 0.5, css: "#2e7d32" },
  { name: "Niebieski", value: 0.25, css: "#1565c0" },
  { name: "Fioletowy", value: 0.1, css: "#6a1b9a" },
  { name: "Szary", value: 0.05, css: "#757575" },
  { name: "Z³oty", value: 5, css: "#c9a227" },
  { name: "Srebrny", value: 10, css: "#b0bec5" }
];

const bands = {
  1: { stripe: stripe1, options: digitColors, title: "Opaska 1" },
  2: { stripe: stripe2, options: digitColors, title: "Opaska 2" },
  3: { stripe: stripe3, options: multiplierColors, title: "Opaska 3 (mno¿nik)" },
  4: { stripe: stripe4, options: toleranceColors, title: "Opaska 4 (tolerancja)" }
};

const selected = {
  1: null,
  2: null,
  3: null,
  4: null
};

function applyStripeColor(el, color) {
  el.setAttribute("fill", color || "url(#bandEmpty)");
}

function formatOhms(value) {
  if (value >= 1000000) return `${value / 1000000} MOhm`;
  if (value >= 1000) return `${value / 1000} kOhm`;
  return `${value} Ohm`;
}

function updateResult() {
  const b1 = selected[1];
  const b2 = selected[2];
  const b3 = selected[3];
  const b4 = selected[4];

  applyStripeColor(stripe1, b1?.css);
  applyStripeColor(stripe2, b2?.css);
  applyStripeColor(stripe3, b3?.css);
  applyStripeColor(stripe4, b4?.css);

  if (!b1 || !b2 || !b3 || !b4) {
    result.textContent = "Rezystancja: wybierz kolory wszystkich pasków.";
    return;
  }

  const resistance = (b1.value * 10 + b2.value) * b3.value;
  result.textContent = `Rezystancja: ${formatOhms(resistance)} (+/- ${b4.value}%)`;
}

function openPalette(bandNumber) {
  const config = bands[bandNumber];
  paletteTitle.textContent = `Wybierz kolor: ${config.title}`;
  paletteOptions.innerHTML = "";

  config.options.forEach((opt) => {
    const btn = document.createElement("button");
    btn.type = "button";
    btn.className = "palette-btn";
    btn.innerHTML = `<span class="swatch" style="background:${opt.css}"></span>${opt.name}`;
    btn.addEventListener("click", () => {
      selected[bandNumber] = opt;
      palette.hidden = true;
      updateResult();
    });
    paletteOptions.appendChild(btn);
  });

  palette.hidden = false;
}

function handleBandKeydown(event, bandNumber) {
  if (event.key === "Enter" || event.key === " ") {
    event.preventDefault();
    openPalette(bandNumber);
  }
}

stripe1.addEventListener("click", () => openPalette(1));
stripe2.addEventListener("click", () => openPalette(2));
stripe3.addEventListener("click", () => openPalette(3));
stripe4.addEventListener("click", () => openPalette(4));

stripe1.addEventListener("keydown", (e) => handleBandKeydown(e, 1));
stripe2.addEventListener("keydown", (e) => handleBandKeydown(e, 2));
stripe3.addEventListener("keydown", (e) => handleBandKeydown(e, 3));
stripe4.addEventListener("keydown", (e) => handleBandKeydown(e, 4));

closePalette.addEventListener("click", () => {
  palette.hidden = true;
});

updateResult();
