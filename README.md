import streamlit as st
import math

# Page setup (App name: first 2 letters of your name + _PHYHBTU)
APP_TITLE = "RK_PHYHBTU"  # Apne naam ke pehle 2 letters yahan likhein

st.set_page_config(page_title=APP_TITLE, page_icon="🧲")
st.title(f"🧲 {APP_TITLE} - Magnetic Units Converter")
st.write("Convert Magnetic SI Units ↔ CGS Units")

# Conversion factors dictionary (1 SI unit = factor * CGS unit)
conversions = {
    "Magnetic Induction (B)": {
        "si": "tesla (T)", "cgs": "gauss (G)", "factor": 1e4
    },
    "Magnetic Field (H)": {
        "si": "A m⁻¹", "cgs": "oersted (Oe)", "factor": 4 * math.pi * 1e-3
    },
    "Magnetization (M)": {
        "si": "A m⁻¹", "cgs": "emu cm⁻³", "factor": 1e-3
    },
    "Magnetic Polarization (J)": {
        "si": "T", "cgs": "G", "factor": 1e4 / (4 * math.pi)
    },
    "Magnetic Moment (m)": {
        "si": "A m²", "cgs": "emu (G cm³)", "factor": 1e3
    },
    "Magnetic Moment per unit mass (σ)": {
        "si": "A m² kg⁻¹", "cgs": "emu g⁻¹", "factor": 1.0
    },
    "Volume Magnetic Susceptibility (χ)": {
        "si": "dimensionless (SI)", "cgs": "dimensionless (cgs)", "factor": 1 / (4 * math.pi)
    },
    "Mass Magnetic Susceptibility (χ_mass)": {
        "si": "m³ kg⁻¹", "cgs": "emu Oe⁻¹ g⁻¹", "factor": 1e3 / (4 * math.pi)
    },
    "Molar Magnetic Susceptibility (χ_m)": {
        "si": "m³ mol⁻¹", "cgs": "emu Oe⁻¹ g mol⁻¹", "factor": 1e6 / (4 * math.pi)
    },
    "Magnetic Permeability (μ)": {
        "si": "H m⁻¹", "cgs": "G Oe⁻¹", "factor": 1e7 / (4 * math.pi)
    },
    "Magnetic Flux (Φ)": {
        "si": "Weber (Wb)", "cgs": "maxwell (Mx)", "factor": 1e8
    },
    "Magnetic Scalar Potential / MMF (ϕ)": {
        "si": "A", "cgs": "gilbert", "factor": 4 * math.pi / 10
    },
    "Magnetic Vector Potential (A)": {
        "si": "Wb m⁻¹", "cgs": "emu (G cm)", "factor": 1e6
    },
    "Magnetic Pole Strength (p)": {
        "si": "A m", "cgs": "emu (G cm²)", "factor": 10.0
    },
    "Demagnetizing Factor (N)": {
        "si": "dimensionless (SI)", "cgs": "dimensionless (cgs)", "factor": 4 * math.pi
    },
    "Magnetostriction Constant (λ)": {
        "si": "dimensionless (SI)", "cgs": "dimensionless (cgs)", "factor": 1.0
    },
    "Anisotropy Constant (K)": {
        "si": "J m⁻³", "cgs": "erg cm⁻³", "factor": 10.0
    },
    "Magnetostatic Energy (Em)": {
        "si": "J m⁻³", "cgs": "erg cm⁻³", "factor": 10.0
    },
    "Energy Product ((BH)max)": {
        "si": "J m⁻³", "cgs": "erg cm⁻³", "factor": 10.0
    }
}

# UI elements
quantity = st.selectbox("Select Magnetic Quantity:", list(conversions.keys()))
direction = st.radio("Conversion Direction:", ["SI to CGS", "CGS to SI"])

item = conversions[quantity]
from_unit = item["si"] if direction == "SI to CGS" else item["cgs"]
to_unit = item["cgs"] if direction == "SI to CGS" else item["si"]

val = st.number_input(f"Enter value in {from_unit}:", value=1.0, format="%.6e")

# Calculation
if direction == "SI to CGS":
    result = val * item["factor"]
else:
    result = val / item["factor"]

st.success(f"**Result:** {val:g} {from_unit} = **{result:.6e}** {to_unit}")
