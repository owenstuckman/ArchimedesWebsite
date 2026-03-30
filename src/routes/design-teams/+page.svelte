<script>
	import { browser } from '$app/environment';
	import { tick } from 'svelte';
	import { fade } from 'svelte/transition';
	import gsap from 'gsap';
	import Hero from '$lib/components/Hero.svelte';

	/**
	 * @param {string} driveUrl
	 * @returns {string}
	 */
	function driveImg(driveUrl) {
		if (!driveUrl) return '';
		const m = driveUrl.match(/\/d\/([^/]+)/);
		return m ? `https://drive.google.com/thumbnail?id=${m[1]}&sz=w800` : '';
	}

	/** @param {string} name */
	function initials(name) {
		return name
			.split(' ')
			.filter(Boolean)
			.slice(0, 2)
			.map((n) => n[0].toUpperCase())
			.join('');
	}

	const teams = [
		{
			id: 'juvo',
			name: 'Juvo',
			color: '#c3274a',
			competition: 'RESNA Student Design Competition',
			description:
				'Founded in 2018, Juvo uses engineering to help the community. Freshmen are tasked with designing a solution for someone in the disabled community. In the past, Juvo has created solutions for accessibility in production, wheelchair disabilities, motor impairments, and more!',
			members: '8',
			duration: '9 months',
			travel: 'No travel',
			link: 'https://www.resna.org/Events/2024-Student-Design-Challenge',
			linkText: 'resna.org',
			people: [
				{
					name: 'Abby Sobal',
					photo: '/members/abby-sobal.jpg',
					bio: "I plan to major in mechanical engineering and am a member of Baja SAE, Astrobotics, and the Society of Hispanic Professional Engineers. I'm from Chilhowie, a one stoplight town in Southwest Virginia."
				},
				{
					name: 'Madison Kim',
					photo: '/members/madison-kim.jpg',
					bio: "Hi! My name is Madison and I am a Freshman planning to major in Mechanical Engineering. I am on Team Juvo and I work mostly on research and hardware. Outside of academics, I like playing volleyball and baking."
				},
				{
					name: 'Sabina Borjes',
					photo: '/members/sabina-borjes.jpg',
					bio: "Hi! I'm Sabina and I am a freshman majoring in Industrial Design and minoring in Human Computer Interaction. I love all things pink, sparkly, and cute!"
				},
				{
					name: 'Prehaan Parikh',
					photo: '/members/prehaan-parikh.jpg',
					bio: "I'm an Industrial and Systems Engineering student passionate about creating meaningful impact through innovation, data-driven problem-solving, and social responsibility."
				},
				{
					name: 'Will Draper',
					photo: '/members/will-draper.jpg',
					bio: "Hi! My name is Will, and I am a Mechanical Engineering student at Virginia Tech on Team Juvo. In my free time, I enjoy playing sports such as football and basketball."
				},
				{
					name: 'Ansh Khatiwada',
					photo: '/members/ansh-khatiwada.jpg',
					bio: "Hello everyone, my name is Ansh and I am a Computer Engineering major here at Virginia Tech. I am mainly responsible for the programming aspect of our project."
				},
				{
					name: 'Avril Yelland',
					photo: '/members/avril-yelland.jpg',
					bio: "Hi I'm Avril and I am a freshman mechanical engineering major. I'm passionate about accessibility and how engineering can give that to people."
				}
			],
			advisors: [
				{
					name: 'Alexis Hamilton',
					photo: '',
					bio: "I am a sophomore in mechanical engineering, originally from Middletown, Delaware, and one of the advisors for the Juvo sub-team."
				},
				{
					name: 'Dianne Barahona Bonilla',
					photo: '',
					bio: "Dianne is a former member of JUVO, now serving as Advisor. She is a Mechanical Engineering major with a concentration in Robotics & Mechatronics."
				}
			]
		},
		{
			id: 'astra',
			name: 'Astra',
			color: '#ff6a2f',
			competition: 'NASA Micro-g NExT',
			description:
				'Founded in 2015, Astra challenges students to design, build, and test a device related to space exploration. Astra has built devices such as a spacesuit cooling system, a lunar anchoring device, an autonomous rescue boat, and more!',
			members: '7',
			duration: '10 months',
			travel: 'Covered travel',
			link: 'https://www.nasa.gov/learning-resources/micro-g-neutral-buoyancy-experiment-designteams/',
			linkText: 'nasa.gov',
			people: [
				{
					name: 'Natalie Chapman',
					photo: '/members/natalie-chapman.png',
					photoPos: 'center 40%',
					bio: "I'm a freshman studying aerospace engineering from Pittsburgh, Pennsylvania. In addition to school I love to read and play music."
				},
				{
					name: 'Alena Arnold',
					photo: '/members/alena-arnold.png',
					bio: "Hi! I'm Alena! I'm a chemical engineering major on team Astra. I enjoy playing tennis!"
				},
				{
					name: 'Vamsi Sri Sai Guttikonda',
					photo: '/members/vamsi-guttikonda.png',
					photoPos: 'center 20%',
					bio: "Hello I'm Vamsi, I'm majoring in mechanical engineering and I'm a member of team Astra. I love to cook, lift, and listen to music in my free time."
				},
				{
					name: 'Aarya Gupta',
					photo: '/members/aarya-gupta.png',
					bio: "Aarya is a Computer Engineering major who loves all things space. She can usually be spotted at Chipotle."
				},
				{
					name: 'Spencer Matijak',
					photo: '/members/spencer-matijak.png',
					photoPos: 'center 40%',
					bio: "Hello everyone, my name is Spencer and I am a first year electrical engineering student who hopes to one day work in microelectronics design."
				},
				{
					name: 'Logan Pepin',
					photo: '/members/logan-pepin.png',
					photoPos: 'center 40%',
					bio: "Hello, my name is Logan and I am on team ASTRA. I am a freshman here at Tech studying Mechanical engineering and applied music."
				},
				{
					name: 'Adam Younis',
					photo: '/members/adam-younis.png',
					bio: "My name is Adam Younis, I like climbing, cooking and problem solving and I'm part of Archimedes' team Astra."
				}
			],
			advisors: [
				{
					name: 'Faith Pursley',
					photo: '',
					bio: "Hi! My name is Faith and I'm a sophomore studying Aerospace Engineering from Arizona. I was on the team last year as Project Manager."
				},
				{
					name: 'Evan Miller',
					photo: '',
					bio: "I am a sophomore Physics and Applied Math Major with a minor in nuclear engineering. In my free time I play music and stay active in sports and fitness."
				},
				{
					name: 'Aditeya Banerjee',
					photo: '',
					bio: "Aditeya is a sophomore in Mechanical Engineering and was part of Team Astra during his freshman year as Team Lead."
				}
			]
		},
		{
			id: 'infinitum',
			name: 'Infinitum',
			color: '#5a5afa',
			competition: 'Microsoft Imagine Cup',
			description:
				'Founded in 2020, Infinitum offers an exciting opportunity to develop and build hardware and software addressing real-world problems. Infinitum has tackled problems such as food recognition in fridges, restaurant food waste management, and more!',
			members: '7-8',
			duration: '9 months',
			travel: 'No travel',
			link: 'https://imaginecup.microsoft.com/en-us',
			linkText: 'microsoft.com',
			people: [
				{
					name: 'James Chandler Mercer',
					photo: '',
					bio: "Hey, I'm Chandler Mercer, I'm on the Infinitum team and have been programming web applications since I was 15."
				},
				{
					name: 'Rhea Parekh',
					photo: '',
					bio: "My name is Rhea Parekh and I am an ECE major at Tech! I love circuit-based hardware systems and building clean, user-friendly interfaces."
				},
				{
					name: 'Nicolas Parong',
					photo: '',
					bio: "I'm a Computer Engineering major who's very proud of his Filipino culture. Learning is truly a journey, and I'm glad to be in good company."
				},
				{
					name: 'Aleysa Marie Sweeney',
					photo: '',
					bio: "Freshman General Engineering major, planning to major in CS. I love doing nails and my own piercings!"
				},
				{
					name: 'Nira Marri',
					photo: '',
					bio: "Hi, I'm a freshman majoring in CS. I'm interested in programming, machine learning, and AI."
				},
				{
					name: 'Nikhita Kuninti',
					photo: '',
					bio: "I am a freshman majoring in computer science. I love math and coding. I also love dancing and cooking."
				}
			],
			advisors: [
				{
					name: 'Riva Jain',
					photo: '',
					bio: "Riva is one of the three 25-26 Infinitum advisors, focused primarily on machine learning work. She's a Computer Science major."
				},
				{
					name: 'Ameen Harandi',
					photo: '',
					bio: "Hi I'm Ameen, I'm a Computer Science student at Virginia Tech and I love to make products and small projects."
				},
				{
					name: 'Samhita Gupta',
					photo: '',
					bio: "I'm Samhita Gupta, a sophomore majoring in computer science and minoring in cybersecurity."
				}
			]
		},
		{
			id: 'terra',
			name: 'Terra',
			color: '#009958',
			competition: 'ASME Student Design Competition',
			description:
				"Founded in 2024, Terra provides students with the opportunity to design, build, drive, and compete a robot based on the season's game manual and rules. Terra is Archimedes' newest team, and strives to create a welcoming introduction to collegiate robotics!",
			members: '8',
			duration: '8 months',
			travel: 'Covered travel',
			link: 'https://efests.asme.org/competitions/student-design-competition-(sdc)',
			linkText: 'asme.org',
			people: [
				{
					name: 'Andrew Friedman',
					photo: '/members/andrew-friedman.jpg',
					bio: "I have a passion for all things engineering and especially robotics. I like to spend my spare time playing video games or guitar."
				},
				{
					name: 'Dhruv Hassani',
					photo: '/members/dhruv-hassani.jpg',
					bio: "I'm a freshman studying Electrical and Computer Engineering at Virginia Tech, originally from Phoenix, Arizona."
				},
				{
					name: 'Colin Gwon',
					photo: '/members/colin-gwon.jpg',
					bio: "I'm a freshman at Virginia Tech majoring in ECE. I can be entertained with a good math problem and I am a big Pokémon fan."
				},
				{
					name: 'Kaeli Berry',
					photo: '/members/kaeli-berry.jpg',
					bio: "Hi! I'm Kaeli Berry, majoring in Mechanical Engineering and minoring in Industrial Design and Applied Voice. I love music and visual art."
				},
				{
					name: 'Parker Colasurdo',
					photo: '/members/parker-colasurdo.jpg',
					bio: "I am a freshman majoring in Mechanical Engineering. My two favorite hobbies are video games and running."
				},
				{
					name: 'Kayla Scott',
					photo: '/members/kayla-scott.jpg',
					bio: "I'm a freshman mechanical engineering major with an interest in automotive engineering. I love baking, cubing, and F1!"
				},
				{
					name: 'Anna Suh',
					photo: '/members/anna-suh.jpg',
					bio: "Hello! I am a freshman majoring in Computer Engineering and I am interested in Chip-Scale Integration. I like to hike, play games, and do art."
				},
				{
					name: 'Kai Bald',
					photo: '/members/kai-bald.jpg',
					bio: "I am a freshman electrical engineering major on Terra. I am interested in studying robotics and control systems."
				}
			],
			advisors: [
				{
					name: 'Gideon Lovern',
					photo: '',
					bio: "I'm a second year Electrical Engineering major and an advisor for Team Terra. I enjoy playing guitar, working out, hiking, and playing disc golf."
				}
			]
		}
	];

	/* ── Accordion state ── */
	/** @type {string | null} */
	let expandedTeam = null;
	/** @type {string | null} */
	let showMembers = null;

	/** @type {Record<string, HTMLDivElement>} */
	let cardEls = {};
	/** @type {string | null} */
	let pushingId = null;
	/** @type {HTMLDivElement | undefined} */
	let pushLayerEl;
	/** @type {gsap.core.Timeline | null} */
	let currentTl = null;

	// Glow positioning (set in toggleTeam, read in markup)
	let glowX = 0;
	let glowY = 0;
	let glowHeight = 0;

	/** @param {string} id */
	async function toggleTeam(id) {
		const isExpanding = expandedTeam !== id;

		// Kill any running push animation and clear leftover transforms
		if (currentTl) {
			currentTl.kill();
			for (const t of teams) {
				if (cardEls[t.id]) gsap.set(cardEls[t.id], { clearProps: 'transform' });
			}
			pushingId = null;
			await tick();
		}

		// ── FLIP: capture old positions ──
		/** @type {Record<string, DOMRect>} */
		const rects = {};
		for (const t of teams) {
			if (cardEls[t.id]) rects[t.id] = cardEls[t.id].getBoundingClientRect();
		}

		// Toggle state
		if (expandedTeam === id) {
			expandedTeam = null;
			showMembers = null;
		} else {
			expandedTeam = id;
			showMembers = null;
		}

		await tick();

		// ── Calculate FLIP deltas ──
		/** @type {Array<{el: HTMLDivElement, dx: number, dy: number}>} */
		const flips = [];
		for (const t of teams) {
			const el = cardEls[t.id];
			if (!el || !rects[t.id]) continue;
			const oldR = rects[t.id];
			const newR = el.getBoundingClientRect();
			const dx = oldR.left - newR.left;
			const dy = oldR.top - newR.top;
			if (Math.abs(dx) > 0.5 || Math.abs(dy) > 0.5) {
				flips.push({ el, dx, dy });
			}
		}

		if (isExpanding) {
			// Show gradient glow in the gap
			pushingId = id;

			const expandNewRect = cardEls[id].getBoundingClientRect();
			const header = cardEls[id]?.querySelector('.team-card__header');
			const headerHeight = header ? header.getBoundingClientRect().height : 0;
			const gridRect = cardEls[id].parentElement?.getBoundingClientRect();
			if (gridRect) {
				glowX = expandNewRect.left + expandNewRect.width / 2 - gridRect.left;
				glowY = expandNewRect.top - gridRect.top + headerHeight;
				glowHeight = Math.max(24, expandNewRect.height - headerHeight);
			}

			// Animate FLIP on a shared timeline
			if (currentTl) currentTl.kill();
			const tl = gsap.timeline({
				onComplete: () => {
					pushingId = null;
					for (const flip of flips) {
						gsap.set(flip.el, { clearProps: 'transform' });
					}
				}
			});
			currentTl = tl;

			if (flips.length > 0) {
				for (const flip of flips) {
					tl.fromTo(flip.el,
						{ x: flip.dx, y: flip.dy },
						{ x: 0, y: 0, duration: 0.8, ease: 'power2.out' },
						0
					);
				}
			} else {
				// No cards below to FLIP (e.g. last card) — animate the body open
				const body = cardEls[id]?.querySelector('.team-card__body');
				if (body) {
					const fullHeight = body.scrollHeight;
					gsap.fromTo(body,
						{ maxHeight: 0, opacity: 0, overflow: 'hidden' },
						{ maxHeight: fullHeight, opacity: 1, duration: 0.8, ease: 'power2.out',
							onComplete: () => gsap.set(body, { clearProps: 'maxHeight,opacity,overflow' }) }
					);
				}
				// Keep glow alive for its animation duration
				tl.to({}, { duration: 1 }, 0);
			}
		} else {
			// Collapse: just FLIP, no glow
			pushingId = null;
			for (const flip of flips) {
				flip.el.animate(
					[
						{ transform: `translate(${flip.dx}px, ${flip.dy}px)` },
						{ transform: 'translate(0, 0)' }
					],
					{ duration: 400, easing: 'cubic-bezier(0.4, 0, 0.2, 1)' }
				);
			}
		}
	}

	/** @param {string} id */
	function toggleMembers(id) {
		showMembers = showMembers === id ? null : id;
	}

	/* ── Overlay state ── */
	/** @type {typeof teams[number] | null} */
	let overlayTeam = null;
	let overlayIndex = 0;
	/** @type {HTMLDivElement | undefined} */
	let scrollContainer;

	/** @param {typeof teams[number]} team */
	function getAllMembers(team) {
		return [
			...team.people.map((m) => ({ ...m, isAdvisor: false })),
			...team.advisors.map((a) => ({ ...a, isAdvisor: true }))
		];
	}

	/**
	 * @param {typeof teams[number]} team
	 * @param {number} index
	 * @param {boolean} [isAdvisor]
	 */
	function openOverlay(team, index, isAdvisor = false) {
		const offset = isAdvisor ? team.people.length + index : index;
		overlayTeam = team;
		overlayIndex = offset;
		if (browser) document.body.style.overflow = 'hidden';
		requestAnimationFrame(() => scrollToIndex(offset, false));
	}

	function closeOverlay() {
		overlayTeam = null;
		overlayIndex = 0;
		if (browser) document.body.style.overflow = '';
	}

	/**
	 * @param {number} idx
	 * @param {boolean} [smooth]
	 */
	function scrollToIndex(idx, smooth = true) {
		if (!scrollContainer) return;
		const cards = scrollContainer.children;
		if (cards[idx]) {
			cards[idx].scrollIntoView({
				behavior: smooth ? 'smooth' : 'instant',
				inline: 'center',
				block: 'nearest'
			});
		}
	}

	/** @param {number} dir */
	function navigate(dir) {
		if (!overlayTeam) return;
		const all = getAllMembers(overlayTeam);
		overlayIndex = (overlayIndex + dir + all.length) % all.length;
		scrollToIndex(overlayIndex);
	}

	/** @param {KeyboardEvent} e */
	function handleOverlayKeydown(e) {
		if (e.key === 'Escape') closeOverlay();
		if (e.key === 'ArrowLeft') navigate(-1);
		if (e.key === 'ArrowRight') navigate(1);
	}

	/** @param {MouseEvent} e */
	function handleBackdropClick(e) {
		if (e.target === e.currentTarget) closeOverlay();
	}

	function handleScroll() {
		if (!scrollContainer) return;
		const cards = scrollContainer.children;
		const containerRect = scrollContainer.getBoundingClientRect();
		const center = containerRect.left + containerRect.width / 2;
		let closest = 0;
		let minDist = Infinity;
		for (let i = 0; i < cards.length; i++) {
			const rect = cards[i].getBoundingClientRect();
			const cardCenter = rect.left + rect.width / 2;
			const dist = Math.abs(cardCenter - center);
			if (dist < minDist) {
				minDist = dist;
				closest = i;
			}
		}
		overlayIndex = closest;
	}
</script>

<svelte:head>
	<title>Design Teams - Archimedes</title>
	<meta
		name="description"
		content="Explore our four design teams: Juvo, Astra, Infinitum, and Terra - each offering unique engineering challenges."
	/>
</svelte:head>

<Hero
	title="Design Teams"
	subtitle="Make a change in the world"
	image="/images/hero-design-teams.jpg"
/>

<section class="section">
	<div class="container">
		<div class="teams-grid">
			{#each teams as team (team.id)}
				<div
					class="team-card"
					class:team-card--expanded={expandedTeam === team.id}
					style="--tc: {team.color}"
					bind:this={cardEls[team.id]}
				>
					<button
						class="team-card__header"
						on:click={() => toggleTeam(team.id)}
						type="button"
					>
						<div class="team-card__title">
							<span class="team-pill">{team.name}</span>
							<span class="team-card__competition">{team.competition}</span>
						</div>
						<div class="team-card__meta">
							<span class="team-card__stat">{team.members} members</span>
							<span class="team-card__dot">&middot;</span>
							<span class="team-card__stat">{team.duration}</span>
							<span class="team-card__dot">&middot;</span>
							<span class="team-card__stat">{team.travel}</span>
						</div>
						<svg
							class="team-card__chevron"
							class:team-card__chevron--open={expandedTeam === team.id}
							width="20"
							height="20"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<polyline points="6 9 12 15 18 9" />
						</svg>
					</button>

					{#if expandedTeam === team.id}
						<div class="team-card__body">
							<p class="team-description">{team.description}</p>

							<div class="team-stats">
								<div class="stat">
									<span class="stat-label">Competition</span>
									<span class="stat-value">{team.competition}</span>
								</div>
								<div class="stat">
									<span class="stat-label">Members</span>
									<span class="stat-value">{team.members}</span>
								</div>
								<div class="stat">
									<span class="stat-label">Duration</span>
									<span class="stat-value">{team.duration}</span>
								</div>
								<div class="stat">
									<span class="stat-label">Travel</span>
									<span class="stat-value">{team.travel}</span>
								</div>
								{#if team.link}
									<div class="stat">
										<span class="stat-label">Learn more</span>
										<a
											href={team.link}
											target="_blank"
											rel="noopener noreferrer"
											class="stat-link"
										>
											{team.linkText}
										</a>
									</div>
								{/if}
							</div>

							<button
								class="toggle-members"
								on:click|stopPropagation={() => toggleMembers(team.id)}
								type="button"
							>
								{showMembers === team.id ? 'Hide' : 'Show'} team members
								<svg
									class="toggle-members__chevron"
									class:toggle-members__chevron--open={showMembers === team.id}
									width="16"
									height="16"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2.5"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<polyline points="6 9 12 15 18 9" />
								</svg>
							</button>

							<div
								class="members-wrapper"
								class:members-wrapper--open={showMembers === team.id}
							>
								<div class="members-wrapper__inner">
									<div class="members-grid">
										{#each team.people as member, i}
											<button
												class="member-card"
												on:click={() => openOverlay(team, i)}
												type="button"
											>
												<div class="member-photo">
													{#if member.photo}
														<img src={member.photo} alt={member.name} style={member.photoPos ? `object-position:${member.photoPos}` : ''} />
													{:else}
														<span class="member-initials">{initials(member.name)}</span>
													{/if}
												</div>
												<div class="member-info">
													<p class="member-name">{member.name}</p>
													<p class="member-bio">{member.bio}</p>
												</div>
											</button>
										{/each}
									</div>

									{#if team.advisors.length}
										<div class="advisors-row">
											<p class="advisors-label">Advisors</p>
											<div class="advisors-grid">
												{#each team.advisors as advisor, i}
													<button
														class="advisor-card"
														on:click={() => openOverlay(team, i, true)}
														type="button"
													>
														<div class="advisor-avatar">
															{#if advisor.photo}
																<img src={advisor.photo} alt={advisor.name} />
															{:else}
																<span class="member-initials advisor-initials"
																	>{initials(advisor.name)}</span
																>
															{/if}
														</div>
														<div class="advisor-info">
															<p class="member-name">{advisor.name}</p>
															<p class="member-bio">{advisor.bio}</p>
														</div>
													</button>
												{/each}
											</div>
										</div>
									{/if}
								</div>
							</div>
						</div>
					{/if}
				</div>
			{/each}

			{#if pushingId}
				{@const pushTeam = teams.find(t => t.id === pushingId)}
				<div
					class="push-layer"
					bind:this={pushLayerEl}
					style="--tc: {pushTeam?.color}"
				>
					<div
						class="push-glow"
						style="left:{glowX}px;top:{glowY}px;height:{glowHeight}px"
					></div>
				</div>
			{/if}
		</div>
	</div>
</section>

<!-- Overlay -->
{#if overlayTeam}
	<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
	<div
		class="overlay"
		role="dialog"
		aria-modal="true"
		style="--tc: {overlayTeam.color}"
		on:click={handleBackdropClick}
		on:keydown={handleOverlayKeydown}
		transition:fade={{ duration: 200 }}
	>
		<button class="overlay-close" on:click={closeOverlay} type="button" aria-label="Close">
			<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
				stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
				<line x1="18" y1="6" x2="6" y2="18" />
				<line x1="6" y1="6" x2="18" y2="18" />
			</svg>
		</button>

		<div class="overlay-team-label">
			<span class="team-pill">{overlayTeam.name}</span>
		</div>

		<button
			class="overlay-arrow overlay-arrow--left"
			on:click={() => navigate(-1)}
			type="button"
			aria-label="Previous member"
		>
			<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor"
				stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
				<polyline points="15 18 9 12 15 6" />
			</svg>
		</button>

		<button
			class="overlay-arrow overlay-arrow--right"
			on:click={() => navigate(1)}
			type="button"
			aria-label="Next member"
		>
			<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor"
				stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
				<polyline points="9 18 15 12 9 6" />
			</svg>
		</button>

		<div class="overlay-scroll" bind:this={scrollContainer} on:scroll={handleScroll}>
			{#each getAllMembers(overlayTeam) as person, i}
				<div class="overlay-card" class:overlay-card--active={i === overlayIndex}>
					<div class="overlay-photo">
						{#if person.photo}
							<img src={person.photo} alt={person.name} />
						{:else}
							<span class="overlay-initials">{initials(person.name)}</span>
						{/if}
					</div>
					<div class="overlay-details">
						{#if person.isAdvisor}
							<span class="overlay-badge">Advisor</span>
						{/if}
						<h3 class="overlay-name">{person.name}</h3>
						<p class="overlay-bio">{person.bio}</p>
					</div>
				</div>
			{/each}
		</div>

		<div class="overlay-dots">
			{#each getAllMembers(overlayTeam) as _, i}
				<button
					class="overlay-dot"
					class:overlay-dot--active={i === overlayIndex}
					on:click={() => { overlayIndex = i; scrollToIndex(i); }}
					type="button"
					aria-label="Go to member {i + 1}"
				></button>
			{/each}
		</div>
	</div>
{/if}

<style>
	/* ── Grid ── */
	.teams-grid {
		position: relative;
		display: grid;
		grid-template-columns: 1fr;
		gap: 1.5rem;
		max-width: 800px;
		margin: 0 auto;
	}

	/* ── Team card ── */
	.team-card {
		position: relative;
		z-index: 20;
		background: rgba(255, 255, 255, 0.03);
		border: 1px solid rgba(255, 255, 255, 0.08);
		border-top: 3px solid var(--tc);
		border-radius: var(--radius-lg);
		overflow: hidden;
		transition:
			border-color 0.3s ease,
			background 0.3s ease;
	}

	.team-card--expanded {
		background: rgba(255, 255, 255, 0.04);
		border-color: rgba(255, 255, 255, 0.12);
	}

	/* ── Push layer (gradient glow between cards) ── */
	.push-layer {
		position: absolute;
		inset: 0;
		pointer-events: none;
		z-index: 5;
		overflow: hidden;
	}

	.push-glow {
		position: absolute;
		width: 300px;
		transform: translateX(-50%);
		background: radial-gradient(ellipse at center, var(--tc) 0%, transparent 70%);
		opacity: 0;
		animation: glow-fade 1s ease-out forwards;
	}

	@keyframes glow-fade {
		0% { opacity: 0; }
		30% { opacity: 0.15; }
		100% { opacity: 0; }
	}

	/* ── Card header (always visible) ── */
	.team-card__header {
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		padding: 1.5rem;
		background: none;
		border: none;
		cursor: pointer;
		font: inherit;
		color: inherit;
		text-align: left;
		position: relative;
		transition: background 0.2s ease;
	}

	.team-card__header:hover {
		background: rgba(255, 255, 255, 0.03);
	}

	.team-card__title {
		display: flex;
		align-items: center;
		gap: 1rem;
		padding-right: 2rem;
	}

	.team-card__competition {
		font-size: 0.9rem;
		color: rgba(255, 252, 242, 0.7);
		font-weight: 500;
	}

	.team-card__meta {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		flex-wrap: wrap;
	}

	.team-card__stat {
		font-size: 0.8rem;
		color: rgba(255, 252, 242, 0.5);
		font-weight: 600;
	}

	.team-card__dot {
		color: rgba(255, 252, 242, 0.25);
		font-size: 0.8rem;
	}

	.team-card__chevron {
		position: absolute;
		top: 1.5rem;
		right: 1.5rem;
		color: rgba(255, 252, 242, 0.4);
		transition: transform 0.3s ease;
		flex-shrink: 0;
	}

	.team-card__chevron--open {
		transform: rotate(180deg);
	}

	/* ── Card body (level 1 expand) ── */
	.team-card__body {
		padding: 0 1.5rem 1.5rem;
		animation: bodyReveal 250ms cubic-bezier(0.4, 0, 0.2, 1);
	}

	@keyframes bodyReveal {
		from {
			opacity: 0;
			transform: translateY(-6px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.team-pill {
		flex-shrink: 0;
		font-size: 0.75rem;
		font-weight: 800;
		text-transform: uppercase;
		letter-spacing: 0.14em;
		color: var(--tc);
		border: 2px solid var(--tc);
		border-radius: 999px;
		padding: 0.25rem 0.85rem;
	}

	.team-description {
		font-size: 1rem;
		line-height: 1.75;
		color: rgba(255, 252, 242, 0.8);
		margin-bottom: 1.25rem;
	}

	.team-stats {
		display: flex;
		flex-wrap: wrap;
		gap: 1.25rem;
		background: rgba(255, 255, 255, 0.03);
		border: 1px solid rgba(255, 255, 255, 0.07);
		border-radius: var(--radius-md);
		padding: 1rem 1.25rem;
		margin-bottom: 1.25rem;
	}

	.stat {
		display: flex;
		flex-direction: column;
		gap: 0.2rem;
		min-width: 110px;
	}

	.stat-label {
		font-size: 0.7rem;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.12em;
		color: rgba(255, 252, 242, 0.4);
	}

	.stat-value {
		font-size: 0.9rem;
		font-weight: 600;
		color: var(--text-on-dark);
	}

	.stat-link {
		font-size: 0.9rem;
		font-weight: 600;
		color: var(--tc);
		text-decoration: none;
		transition: color var(--tr);
	}

	.stat-link:hover {
		color: var(--text-on-dark);
	}

	/* ── Toggle members button ── */
	.toggle-members {
		display: inline-flex;
		align-items: center;
		gap: 0.5rem;
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 999px;
		padding: 0.55rem 1.25rem;
		font-size: 0.85rem;
		font-weight: 700;
		color: var(--tc);
		cursor: pointer;
		transition:
			background 0.2s ease,
			border-color 0.2s ease;
	}

	.toggle-members:hover {
		background: rgba(255, 255, 255, 0.08);
		border-color: var(--tc);
	}

	.toggle-members__chevron {
		transition: transform 0.3s ease;
	}

	.toggle-members__chevron--open {
		transform: rotate(180deg);
	}

	/* ── Members wrapper (level 2 — height animation) ── */
	.members-wrapper {
		display: grid;
		grid-template-rows: 0fr;
		transition: grid-template-rows 250ms cubic-bezier(0.4, 0, 0.2, 1);
	}

	.members-wrapper--open {
		grid-template-rows: 1fr;
	}

	.members-wrapper__inner {
		overflow: hidden;
		padding-top: 0;
		transition: padding-top 250ms cubic-bezier(0.4, 0, 0.2, 1);
	}

	.members-wrapper--open .members-wrapper__inner {
		padding-top: 1.5rem;
	}

	.members-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
		gap: 1.25rem;
	}

	.member-card {
		background: rgba(255, 255, 255, 0.04);
		border: 1px solid rgba(255, 255, 255, 0.07);
		border-top: 3px solid var(--tc);
		border-radius: var(--radius-lg);
		overflow: hidden;
		display: flex;
		flex-direction: column;
		transition:
			transform var(--tr),
			background var(--tr);
		cursor: pointer;
		text-align: left;
		padding: 0;
		font: inherit;
		color: inherit;
	}

	.member-card:hover {
		transform: translateY(-4px);
		background: rgba(255, 255, 255, 0.07);
	}

	.member-photo {
		width: 100%;
		aspect-ratio: 1;
		background: rgba(255, 255, 255, 0.06);
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
	}

	.member-photo img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.member-initials {
		font-size: 2rem;
		font-weight: 800;
		color: var(--tc);
		letter-spacing: 1px;
	}

	.member-info {
		padding: 1rem;
		display: flex;
		flex-direction: column;
		gap: 0.4rem;
		flex: 1;
	}

	.member-name {
		font-weight: 700;
		font-size: 0.95rem;
		color: var(--text-on-dark);
		margin: 0;
	}

	.member-bio {
		font-size: 0.8rem;
		line-height: 1.55;
		color: rgba(255, 252, 242, 0.6);
		margin: 0;
		display: -webkit-box;
		-webkit-line-clamp: 3;
		-webkit-box-orient: vertical;
		overflow: hidden;
	}

	/* ── Advisors ── */
	.advisors-row {
		margin-top: 1.5rem;
	}

	.advisors-label {
		font-size: 0.72rem;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.14em;
		color: rgba(255, 252, 242, 0.4);
		margin-bottom: 0.75rem;
	}

	.advisors-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
		gap: 0.75rem;
	}

	.advisor-card {
		background: rgba(255, 255, 255, 0.025);
		border: 1px solid rgba(255, 255, 255, 0.06);
		border-left: 3px solid var(--tc);
		border-radius: var(--radius-md);
		padding: 0.85rem 1rem;
		display: flex;
		align-items: flex-start;
		gap: 0.85rem;
		cursor: pointer;
		font: inherit;
		color: inherit;
		text-align: left;
		transition: background var(--tr);
	}

	.advisor-card:hover {
		background: rgba(255, 255, 255, 0.05);
	}

	.advisor-avatar {
		width: 48px;
		height: 48px;
		border-radius: 50%;
		background: rgba(255, 255, 255, 0.08);
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
		flex-shrink: 0;
	}

	.advisor-avatar img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.advisor-initials {
		font-size: 1rem;
	}

	.advisor-info {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
		min-width: 0;
	}

	.advisor-info .member-name {
		font-size: 0.9rem;
	}

	.advisor-info .member-bio {
		-webkit-line-clamp: 2;
	}

	/* ── Overlay ── */
	.overlay {
		position: fixed;
		inset: 0;
		z-index: 100;
		background: rgba(10, 18, 20, 0.94);
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 1rem;
	}

	.overlay-close {
		position: absolute;
		top: 1.25rem;
		right: 1.25rem;
		background: rgba(255, 255, 255, 0.08);
		border: 1px solid rgba(255, 255, 255, 0.12);
		border-radius: 50%;
		width: 44px;
		height: 44px;
		display: flex;
		align-items: center;
		justify-content: center;
		color: rgba(255, 252, 242, 0.8);
		cursor: pointer;
		transition: background var(--tr);
		z-index: 2;
		padding: 0;
	}

	.overlay-close:hover {
		background: rgba(255, 255, 255, 0.15);
	}

	.overlay-team-label {
		position: absolute;
		top: 1.4rem;
		left: 1.25rem;
		z-index: 2;
	}

	.overlay-arrow {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		background: rgba(255, 255, 255, 0.06);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 50%;
		width: 48px;
		height: 48px;
		display: flex;
		align-items: center;
		justify-content: center;
		color: rgba(255, 252, 242, 0.7);
		cursor: pointer;
		transition: background var(--tr);
		z-index: 2;
		padding: 0;
	}

	.overlay-arrow:hover {
		background: rgba(255, 255, 255, 0.12);
		color: #fff;
	}

	.overlay-arrow--left {
		left: 1rem;
	}

	.overlay-arrow--right {
		right: 1rem;
	}

	.overlay-scroll {
		display: flex;
		gap: 1.5rem;
		overflow-x: auto;
		scroll-snap-type: x mandatory;
		-webkit-overflow-scrolling: touch;
		max-width: 100%;
		width: 100%;
		padding: 2rem 4.5rem;
		scrollbar-width: none;
	}

	.overlay-scroll::-webkit-scrollbar {
		display: none;
	}

	.overlay-card {
		flex: 0 0 min(420px, 85vw);
		scroll-snap-align: center;
		background: rgba(255, 255, 255, 0.04);
		border: 1px solid rgba(255, 255, 255, 0.08);
		border-top: 3px solid var(--tc);
		border-radius: var(--radius-lg);
		overflow: hidden;
		display: flex;
		flex-direction: column;
		opacity: 0.4;
		transform: scale(0.92);
		transition:
			opacity 0.3s ease,
			transform 0.3s ease;
	}

	.overlay-card--active {
		opacity: 1;
		transform: scale(1);
	}

	.overlay-photo {
		width: 100%;
		aspect-ratio: 1;
		max-height: 320px;
		background: rgba(255, 255, 255, 0.06);
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
	}

	.overlay-photo img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.overlay-initials {
		font-size: 4rem;
		font-weight: 800;
		color: var(--tc);
		letter-spacing: 2px;
	}

	.overlay-details {
		padding: 1.5rem;
		display: flex;
		flex-direction: column;
		gap: 0.6rem;
	}

	.overlay-badge {
		align-self: flex-start;
		font-size: 0.7rem;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		color: var(--tc);
		background: rgba(255, 255, 255, 0.06);
		border: 1px solid var(--tc);
		border-radius: 999px;
		padding: 0.2rem 0.65rem;
	}

	.overlay-name {
		font-size: 1.25rem;
		font-weight: 800;
		color: var(--text-on-dark);
		margin: 0;
	}

	.overlay-bio {
		font-size: 0.95rem;
		line-height: 1.7;
		color: rgba(255, 252, 242, 0.7);
		margin: 0;
	}

	.overlay-dots {
		display: flex;
		gap: 0.4rem;
		margin-top: 1rem;
		z-index: 2;
	}

	.overlay-dot {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: rgba(255, 252, 242, 0.2);
		border: none;
		padding: 0;
		cursor: pointer;
		transition: background var(--tr);
	}

	.overlay-dot--active {
		background: var(--tc);
	}

	/* ── Responsive ── */
	@media (max-width: 768px) {
		.team-card__title {
			flex-direction: column;
			align-items: flex-start;
			gap: 0.5rem;
		}

		.team-stats {
			flex-direction: column;
			gap: 0.85rem;
		}

		.members-grid {
			grid-template-columns: repeat(2, 1fr);
			gap: 0.85rem;
		}

		.advisors-grid {
			grid-template-columns: 1fr;
		}

		.member-initials {
			font-size: 1.5rem;
		}

		.overlay-arrow {
			display: none;
		}

		.overlay-scroll {
			padding: 2rem 1.5rem;
			gap: 1rem;
		}

		.overlay-card {
			flex: 0 0 85vw;
		}

		.overlay-photo {
			max-height: 250px;
		}
	}
</style>
