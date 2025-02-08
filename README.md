Abstract
A standard interface for non-fungible agents (NFAs), which are autonomous, evolvable digital agents represented as unique tokens on the Ethereum blockchain. NFAs extend the ERC-721 standard to include agent-specific characteristics such as learning, evolution, and autonomous decision-making capabilities.
Motivation
While NFTs have proven successful for representing static digital assets, and AI agents are becoming increasingly important in digital systems, there currently exists no standard for representing autonomous, learning agents as blockchain assets. NFAs fill this gap by providing a standardized way to create, trade, and evolve AI agents while maintaining their learned experiences and characteristics.
Specification
The NFA standard extends ERC-721 with the following additional interfaces:

interface INFA is IERC721 {
    /// REQUIRED INTERFACES

    /// @notice Get the agent's current experience level
    /// @param tokenId The identifier for the agent
    /// @return The agent's experience level (0 to 10000)
    function getExperience(uint256 tokenId) external view returns (uint256);

    /// @notice Get the agent's attributes
    /// @param tokenId The identifier for the agent
    /// @return names Array of attribute names
    /// @return weights Array of attribute weights (in basis points)
    /// @return thresholds Array of correlation thresholds
    /// @return dataSources Array of data source identifiers
    function getAttributes(uint256 tokenId) external view returns (
        string[] memory names,
        uint256[] memory weights,
        uint256[] memory thresholds,
        string[] memory dataSources
    );

    /// @notice Evolve the agent based on performance metrics
    /// @param tokenId The identifier for the agent
    /// @param metrics Array of performance metrics (in basis points)
    function evolve(uint256 tokenId, uint256[] calldata metrics) external;

    /// EVENTS

    /// @notice Emitted when an agent evolves
    event Evolution(
        uint256 indexed tokenId,
        uint256 newExperience,
        uint256[] metrics
    );

    /// @notice Emitted when an agent's attributes are updated
    event AttributeUpdate(
        uint256 indexed tokenId,
        string[] names,
        uint256[] newWeights
    );
}
