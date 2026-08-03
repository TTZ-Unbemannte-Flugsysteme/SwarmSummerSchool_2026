# Hardware Overview

Welcome to the Hardware section of the SwarmSummerSchool 2026 drone build. This section contains all the physical component details and assembly guides.

## Table of Contents

- **[Bill of Materials (BOM)](bom.md)**: A complete inventory checklist of all required drone parts, including motors, ESCs, the flight controller, and the companion computer.
- **Assembly Guides**:
  - **[Welding & Soldering Guide](assembly/welding.md)**: Detailed instructions on soldering the XT60 connectors, ESCs, and preparing the Power Distribution Board (PDB).
  - **[Nipping & Wiring Guide](assembly/nipping.md)**: Best practices for wire management, stripping, and securing cables cleanly to the quadcopter frame.
  - **[Motor Mounting](assembly/motors.md)**: Motor identification, fastener sizing, and thread orientation.

<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
    .glass-card {
        background: rgba(15, 23, 42, 0.75);
        backdrop-filter: blur(12px);
        border: 1px solid rgba(255, 255, 255, 0.08);
        box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
    }
</style>

## System Architecture & Interconnect Matrix

<!-- Visual System Diagram Card -->
<div class="lg:col-span-12 glass-card rounded-2xl p-6 border border-slate-800">
    <h3 class="text-lg font-bold text-slate-200 mb-6 text-center flex justify-center items-center">
        <i class="fa-solid fa-network-wired text-sky-400 mr-3"></i> Power & Communication Topology Schema
    </h3>
    
    <div class="flex flex-col gap-8">
        
        <!-- Power Distribution Row -->
        <div class="flex flex-col md:flex-row items-stretch justify-between gap-4 relative">
            
            <!-- Power Source -->
            <div class="w-full md:w-5/12 bg-slate-900 border-2 border-slate-700 rounded-xl p-4 shadow-lg flex flex-col">
                <h4 class="font-bold text-amber-400 mb-4 text-center border-b border-slate-800 pb-2">Power Source (14.8V)</h4>
                <div class="flex flex-col space-y-3 w-full h-full justify-center">
                    <div class="bg-slate-800 rounded p-3 flex flex-col items-center border border-amber-500/30 text-center">
                        <span class="text-sm font-bold text-slate-200">Gens ace 4S 5000mAh LiPo</span>
                        <span class="text-xs text-amber-300 font-mono mt-1">XT90 Output</span>
                    </div>
                    <div class="flex justify-center"><i class="fa-solid fa-arrow-down text-slate-500 text-xs"></i></div>
                    <div class="bg-slate-800 rounded p-2 flex flex-col items-center border border-slate-600/50 text-center">
                        <span class="text-[11px] text-slate-300 font-mono">XT90 Female → XT60 Male Adapter</span>
                    </div>
                    <div class="flex justify-center"><i class="fa-solid fa-arrow-down text-slate-500 text-xs"></i></div>
                    <div class="bg-slate-800 rounded p-3 flex flex-col items-center border border-sky-500/50 text-center shadow-[0_0_15px_rgba(14,165,233,0.15)]">
                        <span class="text-sm font-bold text-sky-400">F450 Main Frame PDB</span>
                    </div>
                </div>
            </div>

            <!-- Connection Lines to Branches -->
            <div class="hidden md:flex flex-col justify-center h-auto w-2/12 relative px-2 min-h-[150px]">
                <!-- A single line coming from PDB dividing into 3 -->
                <div class="absolute top-1/2 left-0 w-1/2 h-0.5 bg-sky-500/50 -translate-y-1/2"></div>
                <div class="absolute top-1/4 bottom-1/4 left-1/2 w-0.5 bg-sky-500/50"></div>
                <div class="absolute top-1/4 left-1/2 w-1/2 h-0.5 bg-sky-500/50 flex items-center justify-end"><i class="fa-solid fa-arrow-right text-sky-400 absolute text-xs -right-1"></i></div>
                <div class="absolute top-1/2 left-1/2 w-1/2 h-0.5 bg-sky-500/50 flex items-center justify-end"><i class="fa-solid fa-arrow-right text-sky-400 absolute text-xs -right-1"></i></div>
                <div class="absolute bottom-1/4 left-1/2 w-1/2 h-0.5 bg-sky-500/50 flex items-center justify-end"><i class="fa-solid fa-arrow-right text-sky-400 absolute text-xs -right-1"></i></div>
            </div>
            
            <div class="flex md:hidden justify-center py-2">
                <i class="fa-solid fa-arrow-down text-sky-500"></i>
            </div>

            <!-- PDB Split Branches -->
            <div class="w-full md:w-5/12 bg-slate-900 border-2 border-slate-700 rounded-xl p-4 shadow-lg flex flex-col justify-center">
                <h4 class="font-bold text-sky-400 mb-4 text-center border-b border-slate-800 pb-2">PDB Split Branches</h4>
                <div class="flex flex-col space-y-4 w-full h-full justify-around py-2">
                    <!-- ESCs -->
                    <div class="bg-slate-800 rounded p-3 flex justify-between items-center border border-emerald-500/40">
                        <div class="flex items-center gap-2">
                            <div class="w-2 h-2 rounded-full bg-emerald-400 shadow-[0_0_8px_rgba(52,211,153,0.6)]"></div>
                            <span class="text-xs font-bold text-emerald-400">4x 30A ESCs</span>
                        </div>
                        <span class="text-[10px] text-slate-400 font-mono">Direct Volts → 2212 Motors</span>
                    </div>
                    <!-- UBEC -->
                    <div class="bg-slate-800 rounded p-3 flex justify-between items-center border border-rose-500/40">
                        <div class="flex items-center gap-2">
                            <div class="w-2 h-2 rounded-full bg-rose-400 shadow-[0_0_8px_rgba(251,113,133,0.6)]"></div>
                            <span class="text-xs font-bold text-rose-400">5V 3A UBEC</span>
                        </div>
                        <span class="text-[10px] text-slate-400 font-mono">Step-Down → Pi 4</span>
                    </div>
                    <!-- FC -->
                    <div class="bg-slate-800 rounded p-3 flex justify-between items-center border border-purple-500/40">
                        <div class="flex items-center gap-2">
                            <div class="w-2 h-2 rounded-full bg-purple-400 shadow-[0_0_8px_rgba(192,132,252,0.6)]"></div>
                            <span class="text-xs font-bold text-purple-400">Matek H743-SLIM</span>
                        </div>
                        <span class="text-[10px] text-slate-400 font-mono">VBAT Pad Power</span>
                    </div>
                </div>
            </div>

        </div>

        <!-- Interconnect Link Row -->
        <div class="bg-slate-900 border-2 border-slate-700 rounded-xl p-4 shadow-lg">
            <h4 class="font-bold text-slate-300 mb-4 text-center text-sm">Data Interconnect Link</h4>
            <div class="flex flex-col md:flex-row items-center justify-between gap-2 px-2">
                <div class="bg-slate-800 border border-rose-500/30 text-rose-400 px-4 py-3 rounded font-bold text-xs flex items-center shadow-[0_0_10px_rgba(225,29,72,0.2)]">
                    <i class="fa-brands fa-raspberry-pi mr-2 text-lg"></i> Raspberry Pi 4 (Companion PC)
                </div>
                
                <div class="flex-1 flex items-center justify-center relative w-full md:w-auto py-4 md:py-0">
                    <div class="absolute w-full h-0.5 bg-sky-400/30"></div>
                    <div class="bg-slate-950 border border-sky-500/50 text-sky-300 px-3 py-1.5 rounded-full text-[10px] font-mono z-10 flex items-center gap-2">
                        <i class="fa-solid fa-right-left"></i>
                        MAVLink2 Serial UART
                        <span class="text-slate-500 ml-1 text-[9px]">(TX1/RX1 ↔ GPIO 14/15)</span>
                    </div>
                </div>

                <div class="bg-slate-800 border border-purple-500/30 text-purple-400 px-4 py-3 rounded font-bold text-xs flex items-center shadow-[0_0_10px_rgba(147,51,234,0.2)]">
                    <i class="fa-solid fa-microchip mr-2 text-lg"></i> Matek H743 FC
                </div>
            </div>
        </div>

    </div>
</div>
