# Roadmap de construcción — Mockup Studio

Orden calculado por dependencias entre módulos (un módulo va después de aquellos a los que referencia). Marca cada uno al terminarlo.

- [ ] **Plataforma** — `.planning/modules/_platform/spec.md` (seguridad, tenants, billing, integraciones)
- [ ] **1. Sistema** — `.planning/modules/sistema/spec.md` · 5 entidades · núcleo · fase 1
- [ ] **2. Catálogo de prendas** — `.planning/modules/catalogo/spec.md` · 7 entidades · depende de: sistema · fase 1
- [ ] **3. Bases de mockup** — `.planning/modules/bases/spec.md` · 3 entidades · depende de: sistema, catalogo · fase 1
- [ ] **4. Diseños** — `.planning/modules/disenos/spec.md` · 5 entidades · depende de: sistema, catalogo · fase 1
- [ ] **5. Inteligencia artificial** — `.planning/modules/ia/spec.md` · 3 entidades · depende de: sistema, disenos · fase 1
- [ ] **6. Mockups y lotes** — `.planning/modules/mockups/spec.md` · 3 entidades · depende de: sistema, bases, disenos, catalogo · fase 1
- [ ] **7. Costos de producción** — `.planning/modules/costos/spec.md` · 4 entidades · depende de: sistema, catalogo, disenos · fase 1
- [ ] **8. Producción** — `.planning/modules/produccion/spec.md` · 2 entidades · depende de: sistema, disenos, catalogo, costos · fase 1
- [ ] **9. Modelos 3D** — `.planning/modules/modelos-3d/spec.md` · 3 entidades · depende de: sistema, catalogo · fase 2