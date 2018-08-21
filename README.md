# WebApi-Imagen-Consumir
Para probar este ejemplo y enviar las imagenes a la web api se puede utilizar https://github.com/elmarkos23/WebApi-Imagen

```aspx-cs
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

namespace WebApi_Imagen_Consumir
{
    public partial class _Default : Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            //ruta de la imagen
            string path = Server.MapPath("~/Images/2.jpg");
            //cargar la imagen en la variable de tipo tyte
            byte[] imageByteData = System.IO.File.ReadAllBytes(path);
            //enviar la imagen por la web api
            funCrear(imageByteData);
        }
        public void funCrear(byte[] ImageData)
        {
            try
            {
                var content = new MultipartFormDataContent();
                //la imagen se carga en el contenido
                content.Add(new StreamContent(new MemoryStream(ImageData)), "Images", "2.jpg");
                // se instancia el objeto httpclient
                var httpClient = new HttpClient();
                //asignacion de la tura de la web api
                //aqui se encuentra el ejemplo complementario para ejecutar el web api
                //https://github.com/elmarkos23/WebApi-Imagen-Consumir

                var uploadServiceBaseAddress = "http://localhost:49526/api/Imagen/Upload";
                //envio a la web api el contenido (la imagen)
                var httpResponseMessage = httpClient.PostAsync(uploadServiceBaseAddress, content);
            }
            catch (Exception ex)
            {
                string a = ex.Message.ToString();
            }
        }
    }
}
```
