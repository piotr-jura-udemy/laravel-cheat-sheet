### Deleting models

To delete a model, call the `delete` method on model instance

```
$post = BlogPost::findOrFail($id);
$post->delete();
```

Alternatively, without loading the model first

```
BlogPost::destroy($id);
```

Or to delete a collection of models at once

```
BlogPost::delete([1, 2, 3]);
```

#### Soft deleting

You may optionally opt to keep the original record in database, and just mark it with `deleted_at` field.

To enable it easily, use the `SoftDeletes` trait on the model

```
namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class BlogPost extends Model
{
    use SoftDeletes;

    protected $dates = ['deleted_at'];
}
```

You need to remember to add the `deleted_at` column to the Model

```
Schema::table('blog_posts', function (Blueprint $table) {
    $table->softDeletes();
});
```

To determine if a particular model instance was deleted use `trashed` method.

```
$isDeleted = $post->trashed();
```

Now when you query for models, the soft deleted models are automatically exlcuded from results.

```
// This will never include models that were "soft deleted"
$posts = BlogPost::all();
```

To include also the "soft deleted" models

```
BlogPost::withTrashed()->get();
```

To fetch only trashed models

```
BlogPost::onlyTrashed()->get();
```

To restore a soft deleted model

```
$post->restore();
```

If a model is "soft deleteable" and you wish to permanently remove it

```
$post->forceDelete();
```
