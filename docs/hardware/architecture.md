# System Architecture & Interconnect Matrix

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

<div class="grid grid-cols-1 lg:grid-cols-12 gap-6 mt-6">
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

    <!-- Pinout Allocation Table -->
    <div class="lg:col-span-12 glass-card rounded-2xl overflow-hidden border border-slate-800">
        <div class="p-4 bg-slate-900/80 border-b border-slate-800">
            <h4 class="text-sm font-bold text-slate-200">Flight Controller & Peripheral Pinout Assignment</h4>
        </div>
        <div class="overflow-x-auto">
            <table class="w-full text-left text-xs text-slate-300 border-collapse">
                <thead>
                    <tr class="bg-slate-900/50 text-slate-400 font-mono border-b border-slate-800">
                        <th class="py-2.5 px-4">Host Component</th>
                        <th class="py-2.5 px-4">Peripheral Device</th>
                        <th class="py-2.5 px-4">Protocol / Bus</th>
                        <th class="py-2.5 px-4">Target FC Port / Pins</th>
                        <th class="py-2.5 px-4">Power Source</th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-slate-800/60 font-mono">
                    <tr class="hover:bg-slate-800/20">
                        <td class="py-2.5 px-4 text-purple-400">Matek H743-SLIM</td>
                        <td class="py-2.5 px-4 text-slate-200">Raspberry Pi 4</td>
                        <td class="py-2.5 px-4 text-sky-400">MAVLink Serial</td>
                        <td class="py-2.5 px-4">UART1 (TX1 / RX1)</td>
                        <td class="py-2.5 px-4 text-amber-400">5V UBEC (GPIO Pin 2/4)</td>
                    </tr>
                    <tr class="hover:bg-slate-800/20">
                        <td class="py-2.5 px-4 text-purple-400">Matek H743-SLIM</td>
                        <td class="py-2.5 px-4 text-slate-200">GEPRC M10 GPS</td>
                        <td class="py-2.5 px-4 text-sky-400">NMEA / UBX UART</td>
                        <td class="py-2.5 px-4">UART2 (TX2 / RX2)</td>
                        <td class="py-2.5 px-4">5V FC Pad</td>
                    </tr>
                    <tr class="hover:bg-slate-800/20">
                        <td class="py-2.5 px-4 text-purple-400">Matek H743-SLIM</td>
                        <td class="py-2.5 px-4 text-slate-200">GEPRC M10 Compass</td>
                        <td class="py-2.5 px-4 text-sky-400">I2C Bus</td>
                        <td class="py-2.5 px-4">I2C1 (SDA1 / SCL1)</td>
                        <td class="py-2.5 px-4">5V FC Pad</td>
                    </tr>
                    <tr class="hover:bg-slate-800/20">
                        <td class="py-2.5 px-4 text-purple-400">Matek H743-SLIM</td>
                        <td class="py-2.5 px-4 text-slate-200">FrSky Archer R8 RX</td>
                        <td class="py-2.5 px-4 text-sky-400">FBUS / SBUS</td>
                        <td class="py-2.5 px-4">RX6 (RC Input Pad)</td>
                        <td class="py-2.5 px-4">5V FC Pad</td>
                    </tr>
                    <tr class="hover:bg-slate-800/20">
                        <td class="py-2.5 px-4 text-purple-400">Matek H743-SLIM</td>
                        <td class="py-2.5 px-4 text-slate-200">4x 30A ESCs</td>
                        <td class="py-2.5 px-4 text-sky-400">PWM Output</td>
                        <td class="py-2.5 px-4">S1, S2, S3, S4 Pads</td>
                        <td class="py-2.5 px-4 text-emerald-400">Direct PDB LiPo</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <!-- Visual Board Reconstruct -->
    <div class="lg:col-span-12 glass-card rounded-2xl p-6 border border-slate-800 mt-4 relative overflow-hidden">
        <h4 class="text-base font-bold text-slate-200 mb-8 text-center flex justify-center items-center">
            <i class="fa-solid fa-microchip text-purple-400 mr-2"></i> STM32H743 (Matek H743-SLIM) Board Visualization
        </h4>
        
        <div class="flex flex-col md:flex-row items-center justify-between gap-6 relative">
            
            <!-- Left Peripherals -->
            <div class="flex flex-col space-y-8 w-full md:w-1/3 z-10">
                <!-- RPi 4 -->
                <div class="bg-slate-900/80 border border-rose-500/30 p-3 rounded-lg flex items-center justify-end shadow-lg transition hover:border-rose-500/60">
                    <div class="mr-3 text-right">
                        <div class="text-[13px] font-bold text-rose-400">Raspberry Pi 4</div>
                        <div class="text-[10px] text-slate-400">MAVLink Serial / 5V UBEC</div>
                    </div>
                    <div class="bg-rose-500/20 text-rose-300 text-[10px] font-mono px-2 py-1 rounded border border-rose-500/30">GPIO 14/15</div>
                    <div class="h-0.5 w-6 sm:w-12 bg-sky-500/40 ml-2 rounded"></div>
                </div>
                
                <!-- GPS & Compass -->
                <div class="bg-slate-900/80 border border-sky-500/30 p-3 rounded-lg flex items-center justify-end shadow-lg transition hover:border-sky-500/60">
                    <div class="mr-3 text-right">
                        <div class="text-[13px] font-bold text-sky-400">GEPRC M10 GPS+Mag</div>
                        <div class="text-[10px] text-slate-400">NMEA + I2C / 5V FC Pad</div>
                    </div>
                    <div class="bg-sky-500/20 text-sky-300 text-[10px] font-mono px-2 py-1 rounded border border-sky-500/30">GPS/I2C</div>
                    <div class="h-0.5 w-6 sm:w-12 bg-sky-500/40 ml-2 rounded"></div>
                </div>
            </div>
            
            <!-- Central Flight Controller (Board) -->
            <div class="w-48 h-64 bg-slate-950 border-2 border-slate-700 rounded-xl relative flex flex-col items-center justify-center shadow-[0_0_40px_rgba(0,0,0,0.6)] z-20">
                <!-- Board Texture lines -->
                <div class="absolute inset-0 opacity-10 bg-[linear-gradient(45deg,transparent_25%,rgba(255,255,255,0.1)_25%,rgba(255,255,255,0.1)_50%,transparent_50%,transparent_75%,rgba(255,255,255,0.1)_75%,rgba(255,255,255,0.1)_100%)] bg-[length:20px_20px]"></div>
                
                <!-- Microcontroller Chip -->
                <div class="w-16 h-16 bg-slate-900 border border-slate-600 rounded flex items-center justify-center mb-6 transform rotate-45 shadow-inner">
                    <div class="text-[7px] text-slate-400 -rotate-45 font-mono text-center leading-tight">
                        <span class="font-bold text-slate-300">STM32</span><br>H743VIT6
                    </div>
                </div>
                <div class="text-center font-bold text-slate-200 z-10 text-sm">Matek H743-SLIM</div>
                <div class="text-[9px] text-slate-500 mt-1 uppercase tracking-wider z-10">Flight Controller</div>
                
                <!-- Left Pads -->
                <div class="absolute left-0 top-8 flex flex-col space-y-10 -ml-2">
                    <div class="bg-sky-400 text-slate-950 text-[9px] font-mono font-bold px-1.5 py-0.5 rounded-sm shadow-[0_0_10px_rgba(56,189,248,0.5)]">UART1<br>TX/RX</div>
                    <div class="bg-sky-400 text-slate-950 text-[9px] font-mono font-bold px-1.5 py-0.5 rounded-sm shadow-[0_0_10px_rgba(56,189,248,0.5)]">UART2<br>I2C1</div>
                </div>
                
                <!-- Right Pads -->
                <div class="absolute right-0 top-12 flex flex-col space-y-10 -mr-2 items-end">
                    <div class="bg-emerald-400 text-slate-950 text-[9px] font-mono font-bold px-1.5 py-0.5 rounded-sm shadow-[0_0_10px_rgba(52,211,153,0.5)]">S1-S4<br>PWM</div>
                    <div class="bg-purple-400 text-slate-950 text-[9px] font-mono font-bold px-1.5 py-0.5 rounded-sm shadow-[0_0_10px_rgba(192,132,252,0.5)]">RX6<br>Pad</div>
                </div>
                
                <!-- USB Port (Top) -->
                <div class="absolute top-0 w-8 h-3 bg-slate-300 border border-slate-400 rounded-b-md shadow-inner"></div>
            </div>
            
            <!-- Right Peripherals -->
            <div class="flex flex-col space-y-8 w-full md:w-1/3 z-10">
                <!-- ESCs -->
                <div class="bg-slate-900/80 border border-emerald-500/30 p-3 rounded-lg flex items-center justify-start shadow-lg transition hover:border-emerald-500/60">
                    <div class="h-0.5 w-6 sm:w-12 bg-emerald-500/40 mr-2 rounded"></div>
                    <div class="bg-emerald-500/20 text-emerald-300 text-[10px] font-mono px-2 py-1 rounded border border-emerald-500/30">PWM Out</div>
                    <div class="ml-3 text-left">
                        <div class="text-[13px] font-bold text-emerald-400">4x 30A ESCs</div>
                        <div class="text-[10px] text-slate-400">Direct PDB LiPo Power</div>
                    </div>
                </div>
                
                <!-- Receiver -->
                <div class="bg-slate-900/80 border border-purple-500/30 p-3 rounded-lg flex items-center justify-start shadow-lg transition hover:border-purple-500/60">
                    <div class="h-0.5 w-6 sm:w-12 bg-purple-500/40 mr-2 rounded"></div>
                    <div class="bg-purple-500/20 text-purple-300 text-[10px] font-mono px-2 py-1 rounded border border-purple-500/30">FBUS/SBUS</div>
                    <div class="ml-3 text-left">
                        <div class="text-[13px] font-bold text-purple-400">FrSky Archer R8</div>
                        <div class="text-[10px] text-slate-400">5V FC Pad Power</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
