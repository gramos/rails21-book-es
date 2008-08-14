## Details

El foco principal de los cambios de Rails fue Ruby 1.9. Aspectos menores fueron analizados para incrementar la compatibilidad de Rails con la nueva versión de Ruby. Detalles como cambiar **File.exists?** por **File.exist?** no fueron dejados de lado.

Además, en Ruby 1.9, el módulo **Base64** (base64.rb) fue eliminado, por esa razón, todas las referencias fueron remplazadas por  **ActiveSupport::Base64**.
