#!/usr/bin/env python3
"""
Allostatic Friction and Hysteretic Autonomic Dynamics Framework
Core Simulation Architecture - Unified Standalone Engine
Author: Dr. Marc B. Nock, DDS
"""

import numpy as np

class AllostaticFriction:
    """
    Computes real-time metabolic friction and trigeminal afferent noise flux
    based on three-dimensional craniofacial architecture parameters.
    """
    def __init__(self, airway_volume, jaw_recession, base_muscle_force=12.5):
        self.airway_volume = max(0.1, airway_volume)  # Avoid division by zero
        self.jaw_recession = max(0.0, jaw_recession)
        self.base_muscle_force = base_muscle_force
        
    def compute_coefficient(self, alpha=0.15, beta=0.04):
        """
        Calculates Caf using the exponential airway constriction ratio
        and the required isometric propping force vectors.
        """
        airway_compromise_ratio = self.jaw_recession / self.airway_volume
        isometric_load = self.base_muscle_force * (1.0 + (self.jaw_recession * 0.5))
        
        c_af = alpha * np.exp(airway_compromise_ratio) + beta * isometric_load
        return float(c_af)

    def get_afferent_noise_flux(self, timestep):
        """
        Simulates the Trigeminal Afferent Deluge (high-frequency static signals).
        """
        base_noise = self.jaw_recession * 1.8
        stochastic_component = np.sin(timestep / 10.0) * 0.2 + np.random.normal(0, 0.05)
        return max(0.0, base_noise + stochastic_component)


class HysteresisStateEngine:
    """
    Models path-dependent state transitions within the brainstem's autonomic routers.
    Implements a discrete non-linear memory trace to dictate vigilance parameters.
    """
    def __init__(self, initial_state=0.1, memory_decay=0.95):
        self.state = initial_state
        self.memory_decay = memory_decay
        self.memory_kernel = []

    def update_state(self, env_input, friction_tax, static_flux, lambda_scale=0.08):
        """
        Advances the state equation factoring in external load, allostatic friction,
        and historical path memory.
        """
        # Retain history
        self.memory_kernel.append(self.state)
        if len(self.memory_kernel) > 100:
            self.memory_kernel.pop(0)
            
        # Calculate historical convolution trace
        history_trace = sum([val * np.exp(-lambda_scale * (len(self.memory_kernel) - idx)) 
                             for idx, val in enumerate(self.memory_kernel)])
        
        # Calculate net directional driving force
        driving_force = env_input + (friction_tax * 0.4) + (static_flux * 0.15)
        
        # Differential approximation loop with a non-linear sigmoid ceiling
        dx = 0.12 * (driving_force - (0.5 * self.state)) + (0.02 * history_trace)
        
        # Advance and clip state to hard biological boundaries [0, 1]
        self.state = np.clip(self.state + dx, 0.0, 1.0)
        return float(self.state)


def execute_simulation_run():
    print("[SYSTEM INITIATION] Launching Allostatic Friction & Hysteretic Loop Engine...\n")
    print("=" * 80)
    print("SIMULATION MODEL: Software Stress Sabbatical vs. Hardware Structural Anchor")
    print("=" * 80)
    
    # Define a structurally compromised patient profile (Narrow airway, high jaw recession)
    compromised_hardware = {
        'airway_volume': 14.2,      # mm^2 minimum cross section
        'jaw_recession': 8.5        # mm skeletal retrognathia
    }
    
    total_timesteps = 200
    midpoint = total_timesteps // 2
    
    # Generate Timeline: Phase 1 (Acute External Stress) -> Phase 2 (The Sabbatical Protocol)
    timeline_external_stress = np.zeros(total_timesteps)
    timeline_external_stress[:midpoint] = 0.80   # Intense lifestyle/workload input
    timeline_external_stress[midpoint:] = 0.00   # Complete behavioral unburdening (Sabbatical)
    
    # Initialize Core Engines
    friction_layer = AllostaticFriction(
        airway_volume=compromised_hardware['airway_volume'],
        jaw_recession=compromised_hardware['jaw_recession']
    )
    state_engine = HysteresisStateEngine(initial_state=0.25, memory_decay=0.92)
    
    # Run loop
    for t in range(total_timesteps):
        c_af = friction_layer.compute_coefficient()
        static_flux = friction_layer.get_afferent_noise_flux(t)
        
        current_vigilance = state_engine.update_state(
            env_input=timeline_external_stress[t],
            friction_tax=c_af,
            static_flux=static_flux
        )
        
        # Track energetic allocation distributions
        atp_overhead = (c_af * 0.60) + (current_vigilance * 0.40)
        cognitive_bandwidth = max(0.0, 100.0 - (atp_overhead * 85.0))
        
        # Output telemetry at specific milestones
        if t in [10, midpoint - 10, midpoint + 10, total_timesteps - 1]:
            phase_string = "PHASE 1: HIGH LIFESTYLE LOAD" if t < midpoint else "PHASE 2: ENVIRONMENTAL SABBATICAL"
            print(f"\n[{phase_string} | TIMESTEP {t:03d}]")
