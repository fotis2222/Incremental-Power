<script>
	let power = 0;
	let powerMulti = 1;
	let xp = 0;
	let level = 1;
	let levelReq = 5;
	let xpMulti = 1;
	let pp = 0;
	let ppMulti = 1;

	function getPower() {
		power += powerMulti;
		xp += xpMulti;
		while (xp >= levelReq) {
			xp -= levelReq;
			level += 1;
			levelReq = Math.floor(levelReq * 1.2);
		}
	}

	let upgrades = {
		power_1: {
			id: 1,
			cost: 10,
			level: 0,
			costScaling: 1.2,
			buyUpg() {
				if (power >= this.cost) {
					power -= this.cost;
					powerMulti += 1;
					this.level += 1;
					this.cost = Math.floor(this.cost * this.costScaling);
					upgrades = {...upgrades}
				}
			},
		},
		xp_1: {
			id: 2,
			cost: 50,
			level: 0,
			costScaling: 1.2,
			buyUpg() {
				if (power >= this.cost) {
					power -= this.cost;
					xpMulti += 1;
					this.level += 1;
					this.cost = Math.floor(this.cost * this.costScaling);
					upgrades = {...upgrades}
				}
			},
		},
	};

	function buy(upgrade) {
		upgrade.buyUpg()
	}

	function energize() {
		power = 0;
		powerMulti = 1;
		xp = 0;
		level = 1;
		levelReq = 5;
		xpMulti = 1;
		pp += ppMulti * (level - 1);
	}
</script>

<h1>Incremental power!</h1>
<p class="power-display">Power: {power}</p>
<p class="level-display">Level {level} ({xp}/{levelReq})</p>
<button on:click={getPower} class="power-button">Get {powerMulti} power</button> <br>
<button on:click={() => buy(upgrades.power_1)} class="power-button">Power I<br>+100% power earned.<br>Cost: {upgrades.power_1.cost}<br>Level: {upgrades.power_1.level}</button>
<button on:click={() => buy(upgrades.xp_1)} class="power-button">XP I<br>+100% XP earned.<br>Cost: {upgrades.xp_1.cost}<br>Level: {upgrades.xp_1.level}</button>
<hr>
<h2>Energize</h2>
<p>Energize will reset everything so far for energy.</p>
<button class="energize-button">Do it for {level - 1} energy</button>
<p>{pp} PP</p>
<hr>
<h2>Credits</h2>
<p>Code: me</p>
<p>Idea: MrRedShark77 (Pylon of the mass)</p>