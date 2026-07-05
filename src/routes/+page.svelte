<script>
  import {
    CalendarDays,
    Check,
    Copy,
    Download,
    ExternalLink,
    Globe2,
    MapPin,
    Network,
    Pickaxe,
    Sparkles,
    Users,
    WandSparkles
  } from 'lucide-svelte';

  const stats = [
    { label: '成员人数', value: '32人', icon: Users },
    { label: '成立日期', value: '2025.10.24', icon: CalendarDays }
  ];

  const servers = [
    {
      key: 'ningran',
      title: '宁然一隅整合包服',
      ip: '103.231.56.67:25565',
      region: '香港',
      note: '保持常开状态，适合同好一起探索、冒险与建设。',
      accent: 'from-sky-400 to-cyan-300'
    },
    {
      key: 'campus',
      title: '新蒸程',
      ip: 'free-c3.tudouai.cn:20350',
      region: '校园复原',
      note: '围绕校园场景复原与协作创作，欢迎一起添砖加瓦。',
      accent: 'from-blue-500 to-indigo-400'
    }
  ];

  const links = [
    {
      label: 'PCL2',
      href: 'https://www.ifdian.net/a/LTCat',
      icon: Download,
      className: 'from-sky-500 to-blue-600'
    },
    {
      label: 'Aneko官网',
      href: 'https://miku.coffee/',
      icon: Globe2,
      className: 'from-cyan-400 to-sky-600'
    },
    {
      label: 'MUA联盟',
      href: 'https://www.mualliance.cn/',
      icon: Network,
      className: 'from-indigo-500 to-blue-600'
    }
  ];

  let copiedKey = '';

  async function copyServerIp(ip, key) {
    let copied = false;

    try {
      if (navigator?.clipboard?.writeText) {
        try {
          await navigator.clipboard.writeText(ip);
          copied = true;
        } catch {
          copied = false;
        }
      }

      if (!copied) {
        const textarea = document.createElement('textarea');
        textarea.value = ip;
        textarea.setAttribute('readonly', '');
        textarea.style.position = 'fixed';
        textarea.style.left = '-9999px';
        textarea.style.opacity = '0';
        document.body.appendChild(textarea);
        textarea.focus();
        textarea.select();
        copied = document.execCommand('copy');
        document.body.removeChild(textarea);
      }
    } catch {
      copied = false;
    }

    copiedKey = key;
    window.setTimeout(() => {
      if (copiedKey === key) copiedKey = '';
    }, copied ? 1800 : 1200);
  }
</script>

<svelte:head>
  <title>Aneko MC交流组</title>
</svelte:head>

<main class="min-h-screen overflow-hidden bg-[#071a3d] text-slate-100">
  <section class="anime-blue-bg relative isolate px-4 py-6 sm:px-6 lg:px-8">
    <div class="absolute inset-0 -z-10 bg-[radial-gradient(circle_at_18%_8%,rgba(125,211,252,0.45),transparent_30%),radial-gradient(circle_at_84%_18%,rgba(99,102,241,0.42),transparent_28%),linear-gradient(135deg,#081a3f_0%,#0b4a86_46%,#49bff4_100%)]"></div>
    <div class="absolute inset-x-0 top-0 -z-10 h-[540px] bg-[linear-gradient(180deg,rgba(255,255,255,0.18),rgba(255,255,255,0))]"></div>

    <div class="mx-auto flex max-w-6xl flex-col gap-5">
      <header class="glass-panel glow-hover flex flex-col gap-3 p-4 md:flex-row md:items-center md:justify-between">
        <div class="flex items-center gap-3">
          <div class="grid size-12 place-items-center rounded-lg border border-cyan-200/50 bg-white/18 text-cyan-100 shadow-[0_0_28px_rgba(56,189,248,0.34)]">
            <Pickaxe size={25} strokeWidth={2.4} />
          </div>
          <div>
            <p class="text-sm font-semibold text-cyan-100">Aneko 动漫社</p>
            <h1 class="text-2xl font-black tracking-normal text-white sm:text-3xl">
              Aneko MC交流组
            </h1>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-2 sm:flex">
          {#each stats as stat}
            <div class="flex items-center gap-2 rounded-lg border border-white/25 bg-white/16 px-3 py-2 text-sm font-bold text-white shadow-[0_8px_24px_rgba(14,165,233,0.18)] backdrop-blur-md">
              <svelte:component this={stat.icon} size={17} />
              <span>{stat.label}：{stat.value}</span>
            </div>
          {/each}
        </div>
      </header>

      <div class="grid items-stretch gap-5 lg:grid-cols-[1.05fr_0.95fr]">
        <section class="glass-panel glow-hover p-5 sm:p-7">
          <div class="mb-5 inline-flex items-center gap-2 rounded-lg border border-cyan-100/35 bg-cyan-50/14 px-3 py-2 text-sm font-bold text-cyan-50 shadow-[0_0_24px_rgba(103,232,249,0.22)]">
            <Sparkles size={16} />
            校内 Minecraft 同好据点
          </div>

          <div class="space-y-4">
            <h2 class="max-w-3xl text-4xl font-black leading-tight tracking-normal text-white drop-shadow-[0_8px_28px_rgba(15,23,42,0.38)] sm:text-5xl">
              一起在蓝色星空下，进入方块世界。
            </h2>
            <p class="max-w-2xl text-base leading-8 text-blue-50/88 sm:text-lg">
              这里是Aneko动漫社旗下的MC交流组，成立于2025年10月24日，旨在为校内的Minecraft爱好者提供一个共同游玩与交流的平台。目前群内共有成员32人，宁然一隅整合包服保持常开状态，欢迎各位同好加入我们一起探索方块世界。
            </p>
          </div>

          <div class="mt-6 flex flex-wrap gap-3">
            {#each links as link}
              <a
                class={`glow-button inline-flex items-center gap-2 rounded-lg bg-gradient-to-r px-4 py-3 text-sm font-bold text-white transition ${link.className}`}
                href={link.href}
                target="_blank"
                rel="noreferrer"
              >
                <svelte:component this={link.icon} size={18} />
                {link.label}
                <ExternalLink size={15} />
              </a>
            {/each}
          </div>
        </section>

        <aside class="glass-panel glow-hover relative min-h-[360px] overflow-hidden bg-sky-300/10">
          <img
            class="absolute inset-0 h-full w-full object-cover saturate-[1.08]"
            src="/aneko-mc-hero.png"
            alt="动漫风 Minecraft 方块世界插画"
          />
          <div class="absolute inset-0 bg-[linear-gradient(180deg,rgba(14,165,233,0.08)_0%,rgba(8,47,73,0.15)_42%,rgba(8,16,42,0.82)_100%)]"></div>
          <div class="absolute bottom-0 left-0 right-0 p-5 text-white">
            <p class="text-sm font-bold text-cyan-100">Aneko x Minecraft</p>
            <h2 class="mt-1 text-2xl font-black tracking-normal">宁然一隅，常开中</h2>
          </div>
        </aside>
      </div>
    </div>
  </section>

  <section class="relative px-4 pb-10 pt-2 sm:px-6 lg:px-8">
    <div class="mx-auto grid max-w-6xl gap-5 lg:grid-cols-[1.15fr_0.85fr]">
      <div class="grid gap-5 md:grid-cols-2">
        {#each servers as server}
          <article class="glass-panel glow-hover p-5">
            <div class="flex items-start justify-between gap-4">
              <div>
                <p class="inline-flex items-center gap-1 rounded-lg border border-white/20 bg-white/16 px-2 py-1 text-xs font-black text-cyan-50">
                  <MapPin size={14} />
                  {server.region}
                </p>
                <h3 class="mt-4 text-2xl font-black tracking-normal text-white">{server.title}</h3>
              </div>
              <div class={`grid size-11 shrink-0 place-items-center rounded-lg bg-gradient-to-br ${server.accent} text-white shadow-[0_0_30px_rgba(56,189,248,0.36)]`}>
                <Pickaxe size={23} />
              </div>
            </div>

            <div class="mt-5 rounded-lg border border-cyan-100/25 bg-white/14 p-4 shadow-[0_16px_40px_rgba(8,47,73,0.22)] backdrop-blur-xl">
              <p class="text-xs font-bold uppercase tracking-[0.18em] text-cyan-100">Server IP</p>
              <p class="mt-2 break-all font-mono text-2xl font-black tracking-normal text-white">
                {server.ip}
              </p>
              <button
                class={`mt-4 inline-flex w-full items-center justify-center gap-2 rounded-lg px-4 py-3 text-sm font-black transition ${
                  copiedKey === server.key
                    ? 'copy-flash bg-cyan-400 text-slate-950 shadow-[0_0_28px_rgba(103,232,249,0.72)]'
                    : 'glow-button bg-gradient-to-r from-sky-500 to-blue-700 text-white'
                }`}
                type="button"
                onclick={() => copyServerIp(server.ip, server.key)}
              >
                {#if copiedKey === server.key}
                  <Check size={18} />
                  已复制
                {:else}
                  <Copy size={18} />
                  一键复制 IP
                {/if}
              </button>
            </div>

            <p class="mt-4 text-sm font-semibold leading-6 text-blue-50/80">{server.note}</p>
          </article>
        {/each}
      </div>

      <aside class="glass-panel glow-hover p-5">
        <div class="flex items-center gap-3">
          <div class="grid size-10 place-items-center rounded-lg border border-cyan-100/25 bg-white/16 text-cyan-100">
            <WandSparkles size={21} />
          </div>
          <div>
            <p class="text-sm font-bold text-cyan-100">MUA·Minecraft高校联盟</p>
            <h3 class="text-xl font-black tracking-normal text-white">连接更多校园玩家</h3>
          </div>
        </div>

        <div class="mt-5 space-y-3 text-sm leading-7 text-blue-50/78">
          <p>
            交流组面向校内Minecraft爱好者开放，适合整合包游玩、服务器建设、日常技术交流。
          </p>
          <p>
            想先准备启动器、了解动漫社或访问高校联盟，可以从上方按钮直达对应站点。
          </p>
        </div>

        <div class="mt-5 grid gap-3">
          <div class="rounded-lg border border-white/18 bg-white/12 p-4 backdrop-blur-lg">
            <p class="text-xs font-black uppercase tracking-[0.18em] text-cyan-100">Group</p>
            <p class="mt-1 text-lg font-black text-white">Aneko动漫社 · MC交流组</p>
          </div>
          <div class="rounded-lg border border-white/18 bg-white/12 p-4 backdrop-blur-lg">
            <p class="text-xs font-black uppercase tracking-[0.18em] text-cyan-100">Status</p>
            <p class="mt-1 text-lg font-black text-white">整合包服常开，欢迎加入探索</p>
          </div>
        </div>
      </aside>
    </div>
  </section>
</main>
