# SageMath-code1-for-article

precisione_bit = 4000  
phi = (1 + sqrt(5)) / 2

A = 23
B = phi

M = 48 * (10**46) # M = 4.8 * 10^47
soglia_denominatore = 6 * M
soglia_denominatore_sage = Integer(soglia_denominatore)

gamma_sym = log(2) / log(phi)
gamma_approx = gamma_sym.n(prec=precisione_bit)

eta_sym = log(5) / log(phi)
eta_approx = eta_sym.n(prec=precisione_bit)

def distance_from_nearest_integer(x):
    """Calcola la distanza di x dall'intero più vicino, ||x||."""
    
    x = x.n(prec=precisione_bit)
    frac_part = x - floor(x)
    
    return min(frac_part, 1 - frac_part)

cf = continued_fraction(gamma_approx)
convergenti = cf.convergents()

print(f"Soglia Denominatore (6M): {soglia_denominatore_sage}")
print("Ricerca del denominatore q...")

q_trovato = None
indice = 0
max_iter = 120 

for i in range(max_iter):
    try:
        convergente_attuale = convergenti[i]
        q = convergente_attuale.denominator()
        
        if i % 10 == 0 and i > 0: 
             print(f"  Indice {i}: Denominatore = {q}")

        if q > soglia_denominatore_sage:
            q_trovato = q
            indice = i
            break
            
    except IndexError:
        print("Raggiunta la fine delle convergenti per la precisione corrente.")
        break
    except Exception as e:
        print(f"Si è verificato un errore durante la ricerca di q: {e}")
        break

print("\n--- Risultato ---")
if q_trovato is not None:
    print(f"Denominatore q trovato (indice {indice}): {q_trovato}")
    
    eta_q = eta_approx * q_trovato
    distance_eta = distance_from_nearest_integer(eta_q)
    gamma_q = gamma_approx * q_trovato
    distance_gamma = distance_from_nearest_integer(gamma_q)
    
    epsilon = distance_eta - M * distance_gamma
    
    print(f"\nTermini per epsilon (con q={q_trovato}):")
    print(f"  ||eta * q||: {distance_eta.n(digits=10)}")
    print(f"  ||gamma * q||: {distance_gamma.n(digits=10)}")
    print(f"  Valore di epsilon: {epsilon.n()}")
    
    argomento_log = (A * q_trovato) / epsilon
    
    log_base_B = log(B)
    
    risultato_finale = log(argomento_log) / log_base_B
    
    print(f"\n--- Calcolo Finale log(Aq/epsilon) / log(B) ---")
    print(f"  A = {A}, B = phi (circa {B.n(digits=5)})")
    print(f"  log(Base): {log_base_B.n()}")
    print(f"  Valore Finale: {risultato_finale.n()}")
    
else:
    print("Nessun denominatore q trovato con q > soglia. Aumenta la precisione o le iterazioni.")
