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
        <h3 class="text-base font-bold text-slate-200 mb-4 flex items-center">
            <i class="fa-solid fa-network-wired text-sky-400 mr-2"></i> Power & Communication Topology Schema
        </h3>
        
        <div class="bg-slate-950 rounded-xl p-4 sm:p-6 border border-slate-800 font-mono text-xs text-slate-300 overflow-x-auto">
            <div class="min-w-[650px] space-y-4">
                <!-- Power Line Header -->
                <div class="flex justify-center">
                    <div class="bg-amber-500/10 border border-amber-500/30 text-amber-300 rounded-lg px-4 py-2 text-center shadow-lg">
                        <div class="font-bold">Gens ace 4S 5000mAh LiPo Battery (14.8V)</div>
                        <div class="text-[10px] text-amber-400/80">Amass XT90 Output Connector</div>
                    </div>
                </div>
                
                <div class="flex justify-center">
                    <i class="fa-solid fa-arrow-down text-slate-600"></i>
                </div>

                <div class="flex justify-center">
                    <div class="bg-sky-500/10 border border-sky-500/30 text-sky-300 rounded-md px-3 py-1 text-center text-[11px]">
                        XT90 Female $\leftrightarrow$ XT60 Male Adapter Lead (10AWG)
                    </div>
                </div>

                <div class="flex justify-center">
                    <i class="fa-solid fa-arrow-down text-slate-600"></i>
                </div>

                <!-- PDB Main Node -->
                <div class="bg-slate-900 border border-sky-500/40 rounded-xl p-3 text-center text-sky-400 font-bold shadow-md">
                    F450 Main Frame Integrated Power Distribution Board (PDB)
                </div>

                <!-- Split branches -->
                <div class="grid grid-cols-3 gap-4 pt-2">
                    <div class="bg-slate-900/80 border border-slate-800 rounded-lg p-3 text-center space-y-1">
                        <span class="text-emerald-400 font-semibold block text-[11px]">4x 30A ESCs</span>
                        <span class="text-[10px] text-slate-400">Direct LiPo Voltage $\rightarrow$ 2212 Motors</span>
                    </div>
                    <div class="bg-slate-900/80 border border-slate-800 rounded-lg p-3 text-center space-y-1">
                        <span class="text-amber-400 font-semibold block text-[11px]">5V 3A UBEC</span>
                        <span class="text-[10px] text-slate-400">Step-Down Power $\rightarrow$ Raspberry Pi 4</span>
                    </div>
                    <div class="bg-slate-900/80 border border-slate-800 rounded-lg p-3 text-center space-y-1">
                        <span class="text-purple-400 font-semibold block text-[11px]">Matek H743-SLIM FC</span>
                        <span class="text-[10px] text-slate-400">VBAT Pad Power + Battery Sensor</span>
                    </div>
                </div>

                <!-- Interconnect Link between Pi and FC -->
                <div class="mt-4 pt-4 border-t border-slate-800 flex items-center justify-between text-[11px] bg-slate-900/40 p-3 rounded-lg">
                    <div class="flex items-center space-x-2 text-rose-400">
                        <i class="fa-brands fa-raspberry-pi text-base"></i>
                        <span>Raspberry Pi 4 (Companion PC)</span>
                    </div>
                    <div class="px-3 py-1 bg-sky-500/20 text-sky-300 rounded border border-sky-500/30 font-semibold">
                        MAVLink2 Serial UART (TX1/RX1 $\leftrightarrow$ GPIO 14/15)
                    </div>
                    <div class="flex items-center space-x-2 text-purple-400">
                        <i class="fa-solid fa-microchip text-base"></i>
                        <span>Matek H743 Flight Controller</span>
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
