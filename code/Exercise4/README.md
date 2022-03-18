# Code of your exercise

```java
public class NoGetter extends VoidVisitorWithDefaults<Void> {
    
    private List<String> privateFields = new ArrayList<>();
    private List<String> publicGetters = new ArrayList<>();

    @Override
    public void visit(CompilationUnit unit, Void arg) {
        for(TypeDeclaration<?> type : unit.getTypes()) {
            type.accept(this, null);
        }
    }

    public void visitTypeDeclaration(TypeDeclaration<?> declaration, Void arg) {
        if(!declaration.isPublic()) return;
        System.out.println(declaration.getFullyQualifiedName().orElse("[Anonymous]"));
        for (FieldDeclaration fieldDeclaration : declaration.getFields()) {
            fieldDeclaration.accept(this, arg);
        }
        for(MethodDeclaration method : declaration.getMethods()) {
            method.accept(this, arg);
        }
        List<String> noGetters = searchForNoPublicGetter(privateFields, publicGetters);
        for(String noGetter : noGetters) {
            System.out.println("  " + noGetter + " has no getter!");
        }
        privateFields.clear();
        publicGetters.clear();
    }

    @Override
    public void visit(ClassOrInterfaceDeclaration declaration, Void arg) {
        visitTypeDeclaration(declaration, arg);
    }

    @Override
    public void visit(EnumDeclaration declaration, Void arg) {
        visitTypeDeclaration(declaration, arg);
    }

    @Override
    public void visit(FieldDeclaration declaration, Void arg) {
        if(declaration.isPublic()) return;
        privateFields.add(declaration.getVariable(0).getName().toString());
    }

    @Override
    public void visit(MethodDeclaration declaration, Void arg) {
        if(!declaration.isPublic()) return;
        String methodName = declaration.getNameAsString();
        if(methodName.startsWith("get"))
            publicGetters.add(methodName.substring(3).toLowerCase());
    }

    public List<String> searchForNoPublicGetter(List<String> privateFields, List<String> publicGetters) {
        return privateFields.stream()
                .filter(field -> !publicGetters.contains(field))
                .collect(Collectors.toList());
    }
}
```

