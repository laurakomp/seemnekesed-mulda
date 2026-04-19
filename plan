import { useState, useEffect } from ‘react’;
import { ShoppingBag, Sprout, Calendar, MapPin, Sun, Cloud, Flame, Droplet, Package, AlertCircle, Check, Leaf, Home, Heart, Wind, Bug, ThermometerSun } from ‘lucide-react’;

export default function GardenPlan() {
const [activeTab, setActiveTab] = useState(‘overview’);
const [checked, setChecked] = useState({});
const [expanded, setExpanded] = useState({});
const [loaded, setLoaded] = useState(false);

const startDate = new Date(2026, 3, 19);
const today = new Date();
const daysDiff = Math.floor((today - startDate) / (1000 * 60 * 60 * 24));
const currentWeek = Math.min(10, Math.max(1, Math.floor(daysDiff / 7) + 1));

useEffect(() => {
async function load() {
try {
const result = await window.storage.get(‘garden-progress-v2’, true);
if (result?.value) setChecked(JSON.parse(result.value));
} catch (e) {}
setLoaded(true);
setExpanded({ [`week${currentWeek}`]: true });
}
load();
}, []);

const toggle = async (id) => {
const next = { …checked, [id]: !checked[id] };
setChecked(next);
try {
await window.storage.set(‘garden-progress-v2’, JSON.stringify(next), true);
} catch (e) { console.error(e); }
};

const toggleExpand = (id) => setExpanded({ …expanded, [id]: !expanded[id] });

const categories = {
tropical:     { label: ‘Tropical’,      color: ‘#c17a5a’, bg: ‘rgba(193, 122, 90, 0.15)’, text: ‘#8b4a2a’ },
mediterranean:{ label: ‘Mediterranean’, color: ‘#a89968’, bg: ‘rgba(168, 153, 104, 0.18)’, text: ‘#6e5f34’ },
leafy:        { label: ‘Leafy green’,   color: ‘#7a8a6e’, bg: ‘rgba(122, 138, 110, 0.18)’, text: ‘#3d4f3b’ },
brassica:     { label: ‘Brassica’,      color: ‘#7d6b8f’, bg: ‘rgba(125, 107, 143, 0.18)’, text: ‘#4d3a5f’ },
coolherb:     { label: ‘Cool herb’,     color: ‘#8fa380’, bg: ‘rgba(143, 163, 128, 0.2)’,  text: ‘#4a5d3c’ },
root:         { label: ‘Bulb/root’,     color: ‘#b09474’, bg: ‘rgba(176, 148, 116, 0.2)’,  text: ‘#6b5337’ },
};

const Tag = ({ cat, size = ‘sm’ }) => {
const c = categories[cat];
if (!c) return null;
return (
<span
className={`inline-flex items-center gap-1 rounded-full font-body uppercase tracking-wider whitespace-nowrap ${ size === 'sm' ? 'text-[9px] px-1.5 py-0.5' : 'text-[10px] px-2 py-1' }`}
style={{ backgroundColor: c.bg, color: c.text }}
>
<span className=“w-1.5 h-1.5 rounded-full” style={{ backgroundColor: c.color }} />
{c.label}
</span>
);
};

const shopping = {
‘Soil’: [
{ id: ‘s1’, name: ‘Seed-starting mix (Külvimuld)’, spec: ‘10L · Biolan or Kekkilä’, source: ‘local’ },
{ id: ‘s2’, name: ‘Potting soil (Istutusmuld)’, spec: ‘50–70L total’, source: ‘local’ },
{ id: ‘s3’, name: ‘Vermiculite or perlite’, spec: ‘20L (optional, for container mix)’, source: ‘local’ },
{ id: ‘s4’, name: ‘Mulch — straw or bark chips’, spec: ‘1 bag · retains moisture in kale & salad pots’, source: ‘local’ },
],
‘Containers’: [
{ id: ‘c1’, name: ‘Small pots, 7–9 cm’, spec: ‘~40 pieces · first transplant step’, source: ‘local’ },
{ id: ‘c2’, name: ‘Medium pots, 12–15 cm’, spec: ‘~15 pieces · basils' final home’, source: ‘local’ },
{ id: ‘c3’, name: ‘Large tub, min 5L’, spec: ‘1 piece · water spinach (wants wet feet)’, source: ‘local’ },
{ id: ‘c4’, name: ‘Long troughs, 40–60 cm’, spec: ‘2–3 pieces · min 15 cm deep · terrace salads’, source: ‘local’ },
{ id: ‘c5’, name: ‘Large pots, 15–20L’, spec: ‘3–4 pieces or fabric grow bags · kale’, source: ‘local’ },
{ id: ‘c6’, name: ‘Herb pots, 15–20 cm’, spec: ‘a few · rosemary, thyme, oregano, sage’, source: ‘local’ },
],
‘Fertiliser’: [
{ id: ‘f1’, name: ‘Balanced liquid fertiliser’, spec: ‘Biolan Luomu or Substral Universal’, source: ‘local’ },
{ id: ‘f2’, name: ‘Leafy-green feed’, spec: ‘Optional · Biolan has one for salads/herbs’, source: ‘local’ },
],
‘Tools & Accessories’: [
{ id: ‘t1’, name: ‘Plant labels’, spec: ‘30+ · you'll have 6 basils alone to tell apart’, source: ‘local’ },
{ id: ‘t2’, name: ‘Spray bottle / mister’, spec: ‘1 piece · fine mist for pellets’, source: ‘local’ },
{ id: ‘t3’, name: ‘Watering can with fine rose’, spec: ‘1 piece · avoid blasting seedlings’, source: ‘local’ },
{ id: ‘t4’, name: ‘Drip trays / saucers’, spec: ‘match pot sizes · bottom watering’, source: ‘local’ },
{ id: ‘t5’, name: ‘Insect netting / fine mesh’, spec: ‘for kale from mid-June’, source: ‘local’ },
{ id: ‘t6’, name: ‘Small clip fan’, spec: ‘Optional but HIGHLY recommended · prevents damping off’, source: ‘local’ },
{ id: ‘t7’, name: ‘Thermometer (indoor/outdoor)’, spec: ‘Optional · monitor windowsill + terrace temps’, source: ‘local’ },
],
‘Order online (Amazon.de)’: [
{ id: ‘o1’, name: ‘Second grow light (LED bar)’, spec: ‘30–60 cm, full spectrum · strongly recommended’, source: ‘online’ },
{ id: ‘o2’, name: ‘Timer plug’, spec: ‘if grow light doesn't have one built in’, source: ‘online’ },
],
};

const seedPlan = {
startNow: {
title: ‘Start indoors NOW (April 19)’,
icon: Sprout,
items: [
{ id: ‘sn1’, name: ‘All 6 basils’, note: ‘heat mat’, cat: ‘tropical’ },
{ id: ‘sn2’, name: ‘Water spinach’, note: ‘heat mat’, cat: ‘tropical’ },
{ id: ‘sn3’, name: ‘Rosemary, thyme, oregano, sage, marjoram, savory’, note: ‘heat helps woody perennials’, cat: ‘mediterranean’ },
{ id: ‘sn6’, name: ‘Parsley, chives’, note: ‘no heat needed’, cat: ‘coolherb’ },
{ id: ‘sn4a’, name: ‘Fennel’, note: ‘no heat needed’, cat: ‘root’ },
{ id: ‘sn4b’, name: ‘Cut lettuce, oak leaf, iceberg, batavia, romaine’, note: ‘no heat needed’, cat: ‘leafy’ },
{ id: ‘sn4c’, name: ‘Chard’, note: ‘no heat needed’, cat: ‘leafy’ },
{ id: ‘sn5’, name: ‘A few spinach + lamb's lettuce’, note: ‘insurance indoors’, cat: ‘leafy’ },
],
},
startLater: {
title: ‘Start indoors May 3 (Week 3)’,
icon: Leaf,
items: [
{ id: ‘sl1’, name: ‘3–4 kale seeds in Tray D’, note: ‘no heat mat needed’, cat: ‘brassica’ },
],
},
directSow: {
title: ‘Direct sow outdoors (mid-May onwards)’,
icon: Sun,
items: [
{ id: ‘ds1’, name: ‘Arugula’, note: ‘grows fast, don't bother indoors’, cat: ‘leafy’ },
{ id: ‘ds2’, name: ‘Dill, cilantro, chervil’, note: ‘hate transplanting’, cat: ‘coolherb’ },
{ id: ‘ds3’, name: ‘Succession spinach + lamb's lettuce’, note: ‘continuous harvest’, cat: ‘leafy’ },
{ id: ‘ds4’, name: ‘Extra kale (late May)’, note: ‘succession for later harvest’, cat: ‘brassica’ },
],
},
};

const trays = [
{ id: ‘A’, mat: ‘Mat 1’, heat: true, title: ‘Tray A — Basils’, cats: [‘tropical’],
contents: [‘6 basil varieties × 4 pellets = 24’, ‘6 pellets spare’] },
{ id: ‘B’, mat: ‘Mat 1’, heat: true, title: ‘Tray B — Water spinach + warm herbs’, cats: [‘tropical’, ‘mediterranean’],
contents: [‘6 water spinach pellets’, ‘4 each: rosemary, thyme, oregano, sage, marjoram, savory’] },
{ id: ‘C’, mat: ‘Mat 2’, heat: true, title: ‘Tray C — Salads + fennel’, cats: [‘leafy’, ‘root’],
contents: [‘3 each: cut lettuce, oak leaf, iceberg, batavia, romaine, chard’, ‘3 fennel’, ‘Pull off mat once germinated’] },
{ id: ‘D’, mat: ‘No mat’, heat: false, title: ‘Tray D — Cool herbs + kale’, cats: [‘coolherb’, ‘leafy’, ‘brassica’],
contents: [‘4 parsley, 4 chives’, ‘3 spinach, 3 lamb's lettuce’, ‘Add 4 kale pellets in Week 3 (May 3)’] },
];

const weeks = [
{ n: 1, dates: ‘Apr 19–25’, title: ‘Shop & sow’,
tasks: [
{ id: ‘w1t1’, text: ‘Complete shopping list run (Bauhof/Aias)’ },
{ id: ‘w1t2’, text: ‘Order second grow light online’ },
{ id: ‘w1t3’, text: ‘Sow Tray A (basils) on Mat 1’ },
{ id: ‘w1t4’, text: ‘Sow Tray B (water spinach + warm herbs) on Mat 1’ },
{ id: ‘w1t5’, text: ‘Sow Tray C (salads + fennel) on Mat 2’ },
{ id: ‘w1t6’, text: ‘Sow Tray D (cool herbs), no mat’ },
{ id: ‘w1t7’, text: ‘Domes on, grow light 14–16h/day’ },
{ id: ‘w1t8’, text: ‘Mist pellets daily with room-temp water — don't soak’ },
{ id: ‘w1t9’, text: ‘Set up fan (if you got one) for gentle airflow’ },
],
},
{ n: 2, dates: ‘Apr 26 – May 2’, title: ‘Germination watch’,
tasks: [
{ id: ‘w2t1’, text: ‘Crack domes as sprouts emerge (airflow)’ },
{ id: ‘w2t2’, text: ‘Remove domes when most of a tray is up’ },
{ id: ‘w2t3’, text: ‘Move germinated trays off heat mats’ },
{ id: ‘w2t4’, text: ‘Start rotating trays under grow light (6–8h each)’ },
{ id: ‘w2t5’, text: ‘Switch from misting to bottom-watering as sprouts stand up’ },
{ id: ‘w2t6’, text: ‘Watch for leggy stretching — lower light to 5–10 cm above’ },
],
},
{ n: 3, dates: ‘May 3–9’, title: ‘Sow kale + thin seedlings’,
tasks: [
{ id: ‘w3t1’, text: ‘Sow 4 kale pellets in Tray D’ },
{ id: ‘w3t2’, text: ‘Thin each pellet to 1 strongest seedling (scissors, don't pull)’ },
{ id: ‘w3t3’, text: ‘Start weekly feeding at ¼ strength’ },
{ id: ‘w3t4’, text: ‘Water from below — fill tray, drain excess after 30 min’ },
],
},
{ n: 4, dates: ‘May 10–16’, title: ‘First transplant · Ice Saints’,
warning: ‘Ice Saints May 11–15 — NOTHING outside yet’,
tasks: [
{ id: ‘w4t1’, text: ‘Transplant strongest salads + chard to 7–9 cm pots’ },
{ id: ‘w4t2’, text: ‘Water transplants thoroughly with room-temp water’ },
{ id: ‘w4t3’, text: ‘Keep basils + water spinach on warmest windowsill’ },
{ id: ‘w4t4’, text: ‘Continue feeding weekly at ¼ strength’ },
],
},
{ n: 5, dates: ‘May 17–23’, title: ‘Hardening off begins’,
tasks: [
{ id: ‘w5t1’, text: ‘Harden off lettuces, chard, parsley, chives, kale’ },
{ id: ‘w5t2’, text: ‘Day 1: 1h outside · Day 2: 2h · by end of week: full day’ },
{ id: ‘w5t3’, text: ‘Bring in at night all week’ },
{ id: ‘w5t4’, text: ‘Pre-fill terrace troughs with potting soil’ },
{ id: ‘w5t5’, text: ‘Direct sow arugula on terrace’ },
{ id: ‘w5t6’, text: ‘Direct sow dill, cilantro, chervil on terrace’ },
{ id: ‘w5t7’, text: ‘Direct sow succession spinach + lamb's lettuce’ },
{ id: ‘w5t8’, text: ‘Transplant fennel to deep pots’ },
],
},
{ n: 6, dates: ‘May 24–30’, title: ‘Move outdoors’,
tasks: [
{ id: ‘w6t1’, text: ‘Hardy salads + cool herbs → permanent terrace spots’ },
{ id: ‘w6t2’, text: ‘Transplant 3–4 kale plants to large pots on terrace’ },
{ id: ‘w6t3’, text: ‘Direct sow succession kale (4–6 seeds, thin later)’ },
{ id: ‘w6t4’, text: ‘Transplant basils + water spinach to bigger indoor pots’ },
{ id: ‘w6t5’, text: ‘Mulch tops of kale + salad pots to retain moisture’ },
{ id: ‘w6t6’, text: ‘Continue rotating grow light — basils need most light now’ },
{ id: ‘w6t7’, text: ‘If nights >10°C: start hardening off basil on warm afternoons’ },
],
},
{ n: 7, dates: ‘May 31 – Jun 6’, title: ‘First harvests!’,
tasks: [
{ id: ‘w7t1’, text: ‘Cut-and-come-again lettuce harvest likely starts’ },
{ id: ‘w7t2’, text: ‘Pinch basil tops at 4–6 true leaves to force bushing’ },
{ id: ‘w7t3’, text: ‘Succession-sow more arugula and lettuce in troughs’ },
{ id: ‘w7t4’, text: ‘Check terrace pots moisture daily — morning water’ },
],
},
{ n: 8, dates: ‘Jun 7–13’, title: ‘Basil adventures’,
tasks: [
{ id: ‘w8t1’, text: ‘If nights >12°C: basil can visit terrace in daytime’ },
{ id: ‘w8t2’, text: ‘Bump feeding to ½ strength weekly’ },
{ id: ‘w8t3’, text: ‘Inspect basil undersides for aphids (sticky leaves = check)’ },
],
},
{ n: 9, dates: ‘Jun 14–20’, title: ‘Full swing · watch for pests’,
warning: ‘Check kale undersides for cabbage moth eggs (tiny yellow clusters)’,
tasks: [
{ id: ‘w9t1’, text: ‘Net kale plants OR pick eggs/caterpillars weekly’ },
{ id: ‘w9t2’, text: ‘First baby-leaf kale harvest (outer leaves only, keep centre)’ },
{ id: ‘w9t3’, text: ‘Regular lettuce, arugula, spinach harvests’ },
{ id: ‘w9t4’, text: ‘Pinch basil tops again — keep harvesting to prevent flowering’ },
{ id: ‘w9t5’, text: ‘Reduce grow light to 12h/day (or skip on sunny days)’ },
],
},
{ n: 10, dates: ‘Jun 21–27’, title: ‘Succession & summer’,
tasks: [
{ id: ‘w10t1’, text: ‘Pull bolted spinach + lamb's lettuce’ },
{ id: ‘w10t2’, text: ‘Replace with arugula or heat-tolerant lettuce’ },
{ id: ‘w10t3’, text: ‘Fennel should be bulbing up — check progress’ },
{ id: ‘w10t4’, text: ‘First water spinach harvest (cut stems 5 cm above soil)’ },
{ id: ‘w10t5’, text: ‘Water everything DAILY in heat · twice daily if 25°C+’ },
],
},
];

const watering = [
{ stage: ‘Universal rules’, icon: Droplet, accent: ‘#3d4f3b’,
rules: [
‘Always use room-temperature water · cold tap shocks roots’,
‘Water in the morning whenever possible · leaves dry before night’,
‘Avoid splashing foliage, especially on basil and Mediterranean herbs’,
‘Feel the soil before watering · push finger 2 cm in’,
],
},
{ stage: ‘Seedling stage (Weeks 1–4)’, icon: Sprout, accent: ‘#7a8a6e’,
rules: [
‘Mist surface daily until germination · a fine spray, not a drench’,
‘Once sprouts are up: switch to bottom-watering (fill tray, drain after 30 min)’,
‘Pellets should feel like a wrung-out sponge · never soggy’,
‘Dome off as soon as most seeds sprout — trapped humidity = damping off’,
],
},
];

const wateringByPlant = [
{ cat: ‘tropical’, plants: ‘Water spinach’, freq: ‘Constantly wet’,
details: ‘Native to flooded paddies. Can literally stand in water. Keep saucer full. Never let dry. Leaves wilt fast if thirsty.’ },
{ cat: ‘tropical’, plants: ‘Basil (all 6)’, freq: ‘Moist, never dry’,
details: ‘Water when top 1 cm is dry. Water base of plant, not leaves. In summer: likely daily. Yellow leaves = overwatering.’ },
{ cat: ‘mediterranean’, plants: ‘Rosemary, thyme, oregano, sage, marjoram, savory’, freq: ‘Let dry between’,
details: ‘Drought-lovers. Water deeply, then let top 2–3 cm dry completely. Overwatering kills them faster than underwatering. Once weekly is often enough.’ },
{ cat: ‘leafy’, plants: ‘All 10 salads + succession sowings’, freq: ‘Consistently moist’,
details: ‘Never let wilt — bitter taste and bolting. Never soggy — rot. Check terrace pots every morning in June. Shallow roots dry fast in containers.’ },
{ cat: ‘brassica’, plants: ‘Kale’, freq: ‘Deep, 2–3× weekly’,
details: ‘Deep watering encourages deep roots. Mulch heavily around base. In heat: daily check, water when top 2 cm dry. Wilting = immediate water.’ },
{ cat: ‘coolherb’, plants: ‘Parsley, chives, dill, cilantro, chervil’, freq: ‘Moderate, consistent’,
details: ‘Keep soil evenly moist. Don't let dry out — cilantro especially will bolt immediately. Every 1–2 days in warm weather.’ },
{ cat: ‘root’, plants: ‘Fennel’, freq: ‘Deep, consistent’,
details: ‘Needs steady moisture to form good bulbs. Inconsistent watering = stringy bulbs. Deep water 2–3× weekly, mulch around base.’ },
];

const troubleshooting = [
{ id: ‘tr1’, icon: Wind, title: ‘Damping off (seedlings collapse at soil line)’,
signs: ‘Stems thin and dark at base, seedling flops over’,
fix: ‘Prevention beats cure. Run the fan. Don't overwater. Remove domes early. Thin crowded seedlings. Once it starts, affected seedlings can't be saved — toss and improve airflow.’ },
{ id: ‘tr2’, icon: Sun, title: ‘Leggy / stretched seedlings’,
signs: ‘Tall, thin, pale, reaching for light’,
fix: ‘Light is too far away. Drop the grow light to 5–10 cm above tops. Rotate trays under the light more often. A fan also strengthens stems.’ },
{ id: ‘tr3’, icon: Droplet, title: ‘Yellow leaves’,
signs: ‘Lower or older leaves yellowing’,
fix: ‘Usually overwatering (soggy roots). Let dry out more between waterings. If soil feels fine, could be nutrients — start feeding at ¼ strength.’ },
{ id: ‘tr4’, icon: Cloud, title: ‘White fuzzy mould on soil’,
signs: ‘Fuzzy white patches on pellet surface’,
fix: ‘Too wet + poor airflow. Let surface dry fully. Scrape off mould. Increase airflow (fan, crack dome). Usually cosmetic but indicates conditions ripe for damping off.’ },
{ id: ‘tr5’, icon: Bug, title: ‘Aphids on basil / indoor herbs’,
signs: ‘Tiny green/black dots on stems, sticky residue’,
fix: ‘Spray plants firmly with water in the sink. Repeat every 3–4 days. Bad infestation: dilute dish soap spray (1 tsp per litre) on leaves.’ },
{ id: ‘tr6’, icon: Bug, title: ‘Cabbage moths on kale’,
signs: ‘Small yellow/white eggs on leaf undersides, holes in leaves’,
fix: ‘Net the plants (fine mesh) as soon as they're outside. If unnetted: inspect weekly, squash eggs, pick caterpillars by hand.’ },
{ id: ‘tr7’, icon: ThermometerSun, title: ‘Bolting (going to flower)’,
signs: ‘Lettuce, spinach, cilantro suddenly shoot up a tall stem’,
fix: ‘Triggered by heat and long days. Harvest what you can immediately — flavour turns bitter fast. Replace with heat-tolerant varieties or wait for autumn sowings.’ },
{ id: ‘tr8’, icon: AlertCircle, title: ‘Wilting despite moist soil’,
signs: ‘Droopy leaves, soil still wet’,
fix: ‘Root rot from overwatering. Stop watering. Let dry fully. If no recovery in 3 days, repot into fresh dry soil and trim rotten roots.’ },
];

const spots = {
windowsill: {
title: ‘Windowsill · indoors’,
subtitle: ‘South/west · afternoon + evening sun · warm’,
icon: Sun,
groups: [
{ cat: ‘tropical’, plants: [‘6 basil varieties’, ‘Water spinach (stays indoors all summer)’] },
{ cat: ‘mediterranean’, plants: [‘Rosemary, oregano, thyme, sage, marjoram, savory’] },
],
note: ‘Heat-loving & Mediterranean plants. Rotate grow light for basil especially.’,
},
terrace: {
title: ‘Terrace · outdoors’,
subtitle: ‘Morning sun only · sheltered · cooler’,
icon: Cloud,
groups: [
{ cat: ‘leafy’, plants: [‘Fennel in deep pots’, ‘Chard, cut lettuce, lamb's lettuce, oak leaf, iceberg, spinach, batavia, arugula, romaine’] },
{ cat: ‘coolherb’, plants: [‘Parsley, chives, dill, cilantro, chervil’] },
{ cat: ‘brassica’, plants: [‘Kale (3–4 plants, large pots, sheltered from wind)’] },
],
note: ‘Morning-only sun = less bolting, sweeter leaves. Perfect for brassicas and leafy greens.’,
},
};

const allIds = [
…Object.values(shopping).flat().map(i => i.id),
…weeks.flatMap(w => w.tasks.map(t => t.id)),
];
const doneCount = allIds.filter(id => checked[id]).length;
const progress = Math.round((doneCount / allIds.length) * 100);

const styles = `@import url('https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;0,9..144,600;0,9..144,700;1,9..144,400&family=DM+Sans:opsz,wght@9..40,400;9..40,500;9..40,600;9..40,700&display=swap'); .font-display { font-family: 'Fraunces', Georgia, serif; font-variation-settings: 'SOFT' 50, 'opsz' 100; } .font-body { font-family: 'DM Sans', system-ui, sans-serif; } .paper-bg { background-color: #f5f1e8; background-image: radial-gradient(at 12% 18%, rgba(122, 138, 110, 0.08) 0, transparent 45%), radial-gradient(at 88% 82%, rgba(193, 122, 90, 0.06) 0, transparent 45%); } .grain::before { content: ''; position: absolute; inset: 0; background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.35'/%3E%3C/svg%3E"); mix-blend-mode: multiply; opacity: 0.08; pointer-events: none; }`;

const Overview = () => (
<div className="space-y-6">
<div className="relative overflow-hidden rounded-3xl bg-gradient-to-br from-[#3d4f3b] to-[#2a3a28] text-[#f5f1e8] p-6 grain">
<div className="relative">
<p className="font-body text-xs uppercase tracking-[0.2em] opacity-70 mb-2">Currently</p>
<p className="font-display text-5xl leading-none mb-1">Week {currentWeek}</p>
<p className="font-body text-sm opacity-90 mt-2">
{weeks[currentWeek - 1]?.dates} · {weeks[currentWeek - 1]?.title}
</p>
</div>
</div>

```
  <div className="bg-white/60 rounded-2xl p-5 border border-[#d4c9b0]">
    <div className="flex justify-between items-baseline mb-3">
      <p className="font-body text-xs uppercase tracking-[0.15em] text-[#6b6558]">Progress</p>
      <p className="font-display text-2xl text-[#3d4f3b]">{progress}%</p>
    </div>
    <div className="h-2 bg-[#e8dfc8] rounded-full overflow-hidden">
      <div className="h-full bg-gradient-to-r from-[#7a8a6e] to-[#3d4f3b] transition-all duration-500" style={{ width: `${progress}%` }} />
    </div>
    <p className="font-body text-xs text-[#6b6558] mt-2">{doneCount} of {allIds.length} tasks · synced with partner</p>
  </div>

  <div className="grid grid-cols-2 gap-3">
    {[
      { id: 'shopping', icon: ShoppingBag, label: 'Shopping', sub: 'What to buy', color: '#c17a5a' },
      { id: 'seeds', icon: Sprout, label: 'Seeds & Trays', sub: 'Sowing plan', color: '#7a8a6e' },
      { id: 'schedule', icon: Calendar, label: 'Weekly', sub: '10 weeks', color: '#3d4f3b' },
      { id: 'water', icon: Droplet, label: 'Watering', sub: 'By plant type', color: '#5a7a8a' },
      { id: 'spots', icon: MapPin, label: 'Spots', sub: 'Where things go', color: '#a89968' },
      { id: 'fix', icon: Heart, label: 'Troubleshoot', sub: 'Common problems', color: '#8b4a2a' },
    ].map(item => {
      const Icon = item.icon;
      return (
        <button key={item.id} onClick={() => setActiveTab(item.id)} className="bg-white/60 rounded-2xl p-4 border border-[#d4c9b0] text-left hover:bg-white/80 transition">
          <Icon size={18} style={{ color: item.color }} className="mb-2" />
          <p className="font-display text-lg text-[#2a3a28] leading-tight">{item.label}</p>
          <p className="font-body text-xs text-[#6b6558] mt-1">{item.sub}</p>
        </button>
      );
    })}
  </div>

  <div className="bg-[#e8dfc8]/50 rounded-2xl p-5 border border-[#d4c9b0]">
    <p className="font-display text-lg text-[#2a3a28] mb-3">Plant categories</p>
    <div className="flex flex-wrap gap-2">
      {Object.keys(categories).map(cat => <Tag key={cat} cat={cat} size="lg" />)}
    </div>
    <p className="font-body text-xs text-[#6b6558] mt-3">Tags appear throughout so you can spot which watering, soil, and sun conditions apply.</p>
  </div>
</div>
```

);

const Shopping = () => (
<div className="space-y-5">
{Object.entries(shopping).map(([category, items]) => (
<div key={category} className="bg-white/60 rounded-2xl border border-[#d4c9b0] overflow-hidden">
<div className="px-5 pt-4 pb-2">
<p className="font-display text-xl text-[#2a3a28]">{category}</p>
</div>
{items.map(item => (
<button key={item.id} onClick={() => toggle(item.id)}
className=“w-full flex items-start gap-3 px-5 py-3 border-t border-[#e8dfc8] hover:bg-[#f5f1e8]/50 transition text-left”>
<div className={`mt-0.5 w-5 h-5 rounded-md border-2 flex items-center justify-center flex-shrink-0 transition ${ checked[item.id] ? 'bg-[#3d4f3b] border-[#3d4f3b]' : 'border-[#b5ab90] bg-white' }`}>
{checked[item.id] && <Check size={12} className="text-[#f5f1e8]" strokeWidth={3} />}
</div>
<div className="flex-1 min-w-0">
<p className={`font-body text-sm font-medium ${checked[item.id] ? 'text-[#8a8578] line-through' : 'text-[#2a3a28]'}`}>
{item.name}
</p>
<p className="font-body text-xs text-[#6b6558] mt-0.5">{item.spec}</p>
</div>
<span className={`font-body text-[10px] uppercase tracking-wider px-2 py-1 rounded-full whitespace-nowrap ${ item.source === 'local' ? 'bg-[#7a8a6e]/15 text-[#3d4f3b]' : 'bg-[#c17a5a]/15 text-[#8b4a2a]' }`}>
{item.source === ‘local’ ? ‘local’ : ‘online’}
</span>
</button>
))}
</div>
))}
<p className="font-body text-xs text-[#6b6558] text-center pt-2">
Local = Bauhof · Aias · Hortes · Online = Amazon.de
</p>
</div>
);

const Seeds = () => (
<div className="space-y-5">
{Object.values(seedPlan).map((section, idx) => {
const Icon = section.icon;
return (
<div key={idx} className="bg-white/60 rounded-2xl border border-[#d4c9b0] p-5">
<div className="flex items-center gap-2 mb-3">
<Icon size={18} className="text-[#7a8a6e]" />
<p className="font-display text-lg text-[#2a3a28]">{section.title}</p>
</div>
<ul className="space-y-3">
{section.items.map(item => (
<li key={item.id} className="font-body text-sm">
<div className="flex items-start gap-2 mb-1">
<span className="text-[#7a8a6e] mt-1.5">•</span>
<div className="flex-1">
<span className="text-[#2a3a28]">{item.name}</span>
{item.note && <span className="text-[#6b6558] italic"> — {item.note}</span>}
</div>
</div>
{item.cat && <div className="pl-4"><Tag cat={item.cat} /></div>}
</li>
))}
</ul>
</div>
);
})}

```
  <div>
    <div className="flex items-center gap-2 mb-3 px-1">
      <Package size={18} className="text-[#c17a5a]" />
      <p className="font-display text-lg text-[#2a3a28]">Tray allocation</p>
    </div>
    <div className="space-y-3">
      {trays.map(tray => (
        <div key={tray.id} className="bg-white/60 rounded-2xl border border-[#d4c9b0] p-4">
          <div className="flex items-start justify-between gap-3 mb-2">
            <p className="font-display text-base text-[#2a3a28] flex-1">{tray.title}</p>
            <span className={`font-body text-[10px] uppercase tracking-wider px-2 py-1 rounded-full whitespace-nowrap flex items-center gap-1 ${
              tray.heat ? 'bg-[#c17a5a]/15 text-[#8b4a2a]' : 'bg-[#7a8a6e]/15 text-[#3d4f3b]'
            }`}>
              {tray.heat && <Flame size={10} />}
              {tray.mat}
            </span>
          </div>
          {tray.cats && tray.cats.length > 0 && (
            <div className="flex flex-wrap gap-1 mb-3">
              {tray.cats.map(c => <Tag key={c} cat={c} />)}
            </div>
          )}
          <ul className="space-y-1">
            {tray.contents.map((c, i) => (
              <li key={i} className="font-body text-sm text-[#4a463f] flex gap-2">
                <span className="text-[#b5ab90]">›</span>{c}
              </li>
            ))}
          </ul>
        </div>
      ))}
    </div>
  </div>
</div>
```

);

const Schedule = () => (
<div className="space-y-3">
{weeks.map(week => {
const isCurrent = week.n === currentWeek;
const isPast = week.n < currentWeek;
const isOpen = expanded[`week${week.n}`];
const weekDone = week.tasks.filter(t => checked[t.id]).length;
return (
<div key={week.n}
className={`rounded-2xl border overflow-hidden transition ${ isCurrent ? 'bg-[#3d4f3b] border-[#3d4f3b] text-[#f5f1e8]' : isPast ? 'bg-white/40 border-[#d4c9b0] opacity-75' : 'bg-white/60 border-[#d4c9b0]' }`}>
<button onClick={() => toggleExpand(`week${week.n}`)}
className=“w-full px-5 py-4 text-left flex items-center justify-between gap-3”>
<div className="flex items-center gap-3 flex-1 min-w-0">
<div className={`w-10 h-10 rounded-full flex items-center justify-center flex-shrink-0 ${ isCurrent ? 'bg-[#f5f1e8] text-[#3d4f3b]' : 'bg-[#e8dfc8] text-[#3d4f3b]' }`}>
<span className="font-display text-lg leading-none">{week.n}</span>
</div>
<div className="flex-1 min-w-0">
<p className={`font-display text-base leading-tight ${isCurrent ? 'text-[#f5f1e8]' : 'text-[#2a3a28]'}`}>
{week.title}
</p>
<p className={`font-body text-xs mt-0.5 ${isCurrent ? 'opacity-80' : 'text-[#6b6558]'}`}>
{week.dates} · {weekDone}/{week.tasks.length} done
</p>
</div>
</div>
<span className={`text-xl ${isCurrent ? 'text-[#f5f1e8]' : 'text-[#6b6558]'}`}>
{isOpen ? ‘−’ : ‘+’}
</span>
</button>
{isOpen && (
<div className={`px-5 pb-4 space-y-2 ${isCurrent ? 'border-t border-white/20' : 'border-t border-[#e8dfc8]'} pt-3`}>
{week.warning && (
<div className={`flex items-start gap-2 rounded-xl p-3 mb-2 ${isCurrent ? 'bg-[#c17a5a]/30' : 'bg-[#c17a5a]/15'}`}>
<AlertCircle size={14} className={isCurrent ? ‘text-[#f5c8a8] mt-0.5’ : ‘text-[#8b4a2a] mt-0.5’} />
<p className={`font-body text-xs ${isCurrent ? 'text-[#f5c8a8]' : 'text-[#8b4a2a]'}`}>{week.warning}</p>
</div>
)}
{week.tasks.map(task => (
<button key={task.id} onClick={() => toggle(task.id)}
className=“w-full flex items-start gap-3 py-2 text-left rounded-lg hover:bg-white/10 px-2 -mx-2 transition”>
<div className={`mt-0.5 w-5 h-5 rounded-md border-2 flex items-center justify-center flex-shrink-0 transition ${ checked[task.id] ? isCurrent ? 'bg-[#f5f1e8] border-[#f5f1e8]' : 'bg-[#3d4f3b] border-[#3d4f3b]' : isCurrent ? 'border-[#f5f1e8]/50 bg-transparent' : 'border-[#b5ab90] bg-white' }`}>
{checked[task.id] && <Check size={12} className={isCurrent ? ‘text-[#3d4f3b]’ : ‘text-[#f5f1e8]’} strokeWidth={3} />}
</div>
<p className={`font-body text-sm flex-1 ${ checked[task.id] ? isCurrent ? 'opacity-60 line-through' : 'text-[#8a8578] line-through' : isCurrent ? 'text-[#f5f1e8]' : 'text-[#2a3a28]' }`}>{task.text}</p>
</button>
))}
</div>
)}
</div>
);
})}
</div>
);

const Watering = () => (
<div className="space-y-5">
{watering.map((section, idx) => {
const Icon = section.icon;
return (
<div key={idx} className="bg-white/60 rounded-2xl border border-[#d4c9b0] p-5">
<div className="flex items-center gap-2 mb-3">
<Icon size={18} style={{ color: section.accent }} />
<p className="font-display text-lg text-[#2a3a28]">{section.stage}</p>
</div>
<ul className="space-y-2">
{section.rules.map((r, i) => (
<li key={i} className="font-body text-sm text-[#4a463f] flex gap-2">
<span style={{ color: section.accent }}>›</span>
<span>{r}</span>
</li>
))}
</ul>
</div>
);
})}

```
  <div>
    <p className="font-display text-lg text-[#2a3a28] mb-3 px-1">By plant type</p>
    <div className="space-y-3">
      {wateringByPlant.map((p, i) => {
        const c = categories[p.cat];
        return (
          <div key={i} className="bg-white/60 rounded-2xl border-l-4 border border-[#d4c9b0] p-4" style={{ borderLeftColor: c.color }}>
            <div className="flex items-start justify-between gap-2 mb-2">
              <div className="flex-1">
                <p className="font-display text-base text-[#2a3a28] leading-tight">{p.plants}</p>
                <div className="mt-1"><Tag cat={p.cat} /></div>
              </div>
              <span className="font-body text-xs font-medium px-2 py-1 rounded-full whitespace-nowrap" style={{ backgroundColor: c.bg, color: c.text }}>
                {p.freq}
              </span>
            </div>
            <p className="font-body text-sm text-[#4a463f] leading-relaxed">{p.details}</p>
          </div>
        );
      })}
    </div>
  </div>

  <div className="bg-[#3d4f3b] rounded-2xl p-5 text-[#f5f1e8]">
    <p className="font-display text-base mb-2">Container rule of thumb</p>
    <p className="font-body text-sm opacity-90 leading-relaxed">
      Container soil dries 2–3× faster than garden soil. In June heat, terrace pots may need water morning AND evening. Stick your finger 2 cm into the soil — if dry, water. If damp, wait.
    </p>
  </div>
</div>
```

);

const Troubleshoot = () => (
<div className="space-y-3">
<p className="font-body text-sm text-[#6b6558] px-1 mb-2">
The 8 most common problems, how to spot them, and what to do.
</p>
{troubleshooting.map(item => {
const Icon = item.icon;
const isOpen = expanded[item.id];
return (
<div key={item.id} className="bg-white/60 rounded-2xl border border-[#d4c9b0] overflow-hidden">
<button onClick={() => toggleExpand(item.id)}
className=“w-full px-5 py-4 text-left flex items-start justify-between gap-3”>
<div className="flex items-start gap-3 flex-1">
<div className="w-9 h-9 rounded-full bg-[#c17a5a]/15 flex items-center justify-center flex-shrink-0">
<Icon size={16} className="text-[#8b4a2a]" />
</div>
<p className="font-display text-base text-[#2a3a28] leading-tight pt-1.5">{item.title}</p>
</div>
<span className="text-xl text-[#6b6558] pt-1">{isOpen ? ‘−’ : ‘+’}</span>
</button>
{isOpen && (
<div className="px-5 pb-4 border-t border-[#e8dfc8] pt-3 space-y-3">
<div>
<p className="font-body text-[10px] uppercase tracking-wider text-[#6b6558] mb-1">Signs</p>
<p className="font-body text-sm text-[#4a463f]">{item.signs}</p>
</div>
<div>
<p className="font-body text-[10px] uppercase tracking-wider text-[#6b6558] mb-1">What to do</p>
<p className="font-body text-sm text-[#4a463f] leading-relaxed">{item.fix}</p>
</div>
</div>
)}
</div>
);
})}
</div>
);

const Spots = () => (
<div className="space-y-4">
{Object.entries(spots).map(([key, spot]) => {
const Icon = spot.icon;
const isWindow = key === ‘windowsill’;
return (
<div key={key}
className={`rounded-3xl p-6 relative overflow-hidden grain ${ isWindow ? 'bg-gradient-to-br from-[#e8c89a] to-[#c17a5a] text-[#2a1f18]' : 'bg-gradient-to-br from-[#a8b89c] to-[#7a8a6e] text-[#1f2a1c]' }`}>
<div className="relative">
<Icon size={24} className="mb-3" />
<p className="font-display text-2xl leading-tight mb-1">{spot.title}</p>
<p className="font-body text-xs uppercase tracking-[0.15em] opacity-70 mb-4">{spot.subtitle}</p>
<div className="space-y-3 mb-4">
{spot.groups.map((g, i) => (
<div key={i}>
<div className="mb-1.5"><Tag cat={g.cat} /></div>
<ul className="space-y-1">
{g.plants.map((plant, j) => (
<li key={j} className="font-body text-sm flex gap-2">
<Leaf size={14} className="mt-0.5 flex-shrink-0 opacity-70" />
<span>{plant}</span>
</li>
))}
</ul>
</div>
))}
</div>
<p className="font-body text-xs italic opacity-80 border-t border-current/20 pt-3">{spot.note}</p>
</div>
</div>
);
})}
<div className="bg-white/60 rounded-2xl border border-[#d4c9b0] p-5">
<p className="font-display text-base text-[#2a3a28] mb-2">Why this pairing works</p>
<p className="font-body text-sm text-[#4a463f] leading-relaxed">
Heat-loving plants get the warm south/west window. Cool-loving salads and brassicas get the gentler morning-sun terrace — exactly what they’d prefer anyway. Bolting risk is dramatically lower without harsh afternoon sun.
</p>
</div>
</div>
);

const tabs = [
{ id: ‘overview’, label: ‘Home’, icon: Home },
{ id: ‘shopping’, label: ‘Shop’, icon: ShoppingBag },
{ id: ‘seeds’, label: ‘Seeds’, icon: Sprout },
{ id: ‘schedule’, label: ‘Weeks’, icon: Calendar },
{ id: ‘water’, label: ‘Water’, icon: Droplet },
{ id: ‘spots’, label: ‘Spots’, icon: MapPin },
{ id: ‘fix’, label: ‘Fix’, icon: Heart },
];

if (!loaded) {
return (
<div className="min-h-screen paper-bg flex items-center justify-center">
<p className="font-display text-xl text-[#3d4f3b]">Loading garden plan…</p>
</div>
);
}

return (
<div className="min-h-screen paper-bg font-body pb-24">
<style>{styles}</style>

```
  <header className="px-5 pt-8 pb-5 relative">
    <p className="font-body text-[11px] uppercase tracking-[0.25em] text-[#7a8a6e] mb-1">Tallinn · Spring 2026</p>
    <h1 className="font-display text-4xl text-[#2a3a28] leading-[0.95] tracking-tight">
      The <em className="italic">Garden</em><br />Plan
    </h1>
    <div className="absolute right-5 top-8 w-12 h-12 rounded-full bg-[#3d4f3b] flex items-center justify-center">
      <Droplet size={20} className="text-[#f5f1e8]" />
    </div>
  </header>

  <main className="px-5">
    {activeTab === 'overview' && <Overview />}
    {activeTab === 'shopping' && <Shopping />}
    {activeTab === 'seeds' && <Seeds />}
    {activeTab === 'schedule' && <Schedule />}
    {activeTab === 'water' && <Watering />}
    {activeTab === 'spots' && <Spots />}
    {activeTab === 'fix' && <Troubleshoot />}
  </main>

  <nav className="fixed bottom-0 left-0 right-0 bg-[#f5f1e8]/95 backdrop-blur-md border-t border-[#d4c9b0] px-1 py-2 z-10">
    <div className="flex justify-around max-w-md mx-auto">
      {tabs.map(tab => {
        const Icon = tab.icon;
        const active = activeTab === tab.id;
        return (
          <button key={tab.id} onClick={() => setActiveTab(tab.id)}
            className={`flex flex-col items-center gap-1 px-2 py-2 rounded-xl transition flex-1 ${
              active ? 'bg-[#3d4f3b] text-[#f5f1e8]' : 'text-[#6b6558]'
            }`}>
            <Icon size={16} />
            <span className="font-body text-[9px] font-medium">{tab.label}</span>
          </button>
        );
      })}
    </div>
  </nav>
</div>
```

);
}
